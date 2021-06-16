### cifar 이미지 다운로드
[여기서 다운로드함](https://github.com/YoongiKim/CIFAR-10-images/tree/master/train)  

### efficientNet 기반 classification
[참고한 블로그](https://keep-steady.tistory.com/35)
ImageNet DB 기반 학습한 efficientNet 모델을 끝 2개 레이어 fully connected layer 을 추가 학습하여(-> transferleanning) cifatDB을 분류함  

```
import torch
import torchvision
from torchvision import datasets, models, transforms
import os, time, copy
import torch.distributed as dist
import numpy as np
import matplotlib.pyplot as plt
#dist.init_process_group ( 'gloo', init_method = 'file : /// tmp / somefile', rank = 0, world_size = 1)
dist.init_process_group ( 'gloo', init_method = 'file:///tmp/somefile', rank = 0, world_size = 1)

device = 'cuda:0'

# call model
from efficientnet_pytorch import EfficientNet
model = EfficientNet.from_pretrained('efficientnet-b0').to(device)

# fc 제외하고 freeze
for n, p in model.named_parameters():
    if '_fc' not in n:
        p.requires_grad = False
model = torch.nn.parallel.DistributedDataParallel(model)

DataDir = '/home/jimin/HDD1/tf_test_jm/CIFAR-10-images'
traindir = os.path.join(DataDir, 'train')
valdir = os.path.join(DataDir, 'test')
normalize = transforms.Normalize(mean=[0.485, 0.456, 0.406],
                                     std=[0.229, 0.224, 0.225])

dataloaders, batch_num = {}, {}
dataloaders['train'] = torch.utils.data.DataLoader(
        datasets.ImageFolder(traindir, transforms.Compose([
            transforms.Resize((224,224)),
            transforms.ToTensor(),
            normalize,
        ])),
        batch_size=8, shuffle=True,
        num_workers=4, pin_memory=True)

dataloaders['valid'] = torch.utils.data.DataLoader(
        datasets.ImageFolder(valdir, transforms.Compose([
            transforms.Resize((224,224)),
            transforms.ToTensor(),
            normalize,
        ])),
        batch_size=8, shuffle=False,
        num_workers=4, pin_memory=True)

print('    Total params: %.2fM' % (sum(p.numel() for p in model.parameters())/1000000.0))
# define loss function (criterion) and optimizer
criterion = torch.nn.CrossEntropyLoss().cuda()
optimizer_ft = torch.optim.SGD(model.parameters(), lr=1e-1, momentum=0.9, weight_decay=1e-4)
# exp_lr_scheduler: 조금씩 lr이 줄어들도록
lmbda = lambda epoch: 0.98739
exp_lr_scheduler = torch.optim.lr_scheduler.MultiplicativeLR(optimizer_ft, lr_lambda=lmbda)

batch_num['train'], batch_num['valid'] = len(dataloaders['train']), len(dataloaders['valid'])
print('batch_size : %d,  tvt : %d / %d' % (8, batch_num['train'], batch_num['valid']))

## 데이타 체크
import torchvision
def imshow(inp, title=None):
    """Imshow for Tensor."""
    inp = inp.numpy().transpose((1, 2, 0))
    mean = np.array([0.485, 0.456, 0.406])
    std = np.array([0.229, 0.224, 0.225])
    inp = std * inp + mean
    inp = np.clip(inp, 0, 1)
    plt.imshow(inp)
    if title is not None:
        plt.title(title)
    plt.pause(0.1)  # pause a bit so that plots are updated

num_show_img = 5

class_names = {
    "0": "airpne",
    "1": "automobile",
    "2": "bird",
    "3": "cat",
    "4": "deer",
    "5": "dog",
    "6": "frog",
    "7": "horse",
    "8": "ship",
    "9": "truck"
}
## 이미지 확인 체크
# # train check
# inputs, classes = next(iter(dataloaders['train']))
# out = torchvision.utils.make_grid(inputs[:num_show_img])  # batch의 이미지를 오려부친다
# imshow(out, title=[class_names[str(int(x))] for x in classes[:num_show_img]])
# # valid check
# inputs, classes = next(iter(dataloaders['valid']))
# out = torchvision.utils.make_grid(inputs[:num_show_img])  # batch의 이미지를 오려부친다
# imshow(out, title=[class_names[str(int(x))] for x in classes[:num_show_img]])


def train_model(model, criterion, optimizer, scheduler, num_epochs=25):
    since = time.time()

    best_model_wts = copy.deepcopy(model.state_dict())
    best_acc = 0.0
    train_loss, train_acc, valid_loss, valid_acc = [], [], [], []

    for epoch in range(num_epochs):
        print('Epoch {}/{}'.format(epoch, num_epochs - 1))
        print('-' * 10)

        # Each epoch has a training and validation phase
        for phase in ['train', 'valid']:
            if phase == 'train':
                model.train()  # Set model to training mode
            else:
                model.eval()  # Set model to evaluate mode

            running_loss, running_corrects, num_cnt = 0.0, 0, 0

            # Iterate over data.
            for inputs, labels in dataloaders[phase]:
                inputs = inputs.to(device)
                labels = labels.to(device)

                # zero the parameter gradients
                optimizer.zero_grad()

                # forward
                # track history if only in train
                with torch.set_grad_enabled(phase == 'train'):
                    outputs = model(inputs)
                    _, preds = torch.max(outputs, 1)
                    loss = criterion(outputs, labels)

                    # backward + optimize only if in training phase
                    if phase == 'train':
                        loss.backward()
                        optimizer.step()

                # statistics
                running_loss += loss.item() * inputs.size(0)
                running_corrects += torch.sum(preds == labels.data)
                num_cnt += len(labels)
            if phase == 'train':
                scheduler.step()

            epoch_loss = float(running_loss / num_cnt)
            epoch_acc = float((running_corrects.double() / num_cnt).cpu() * 100)

            if phase == 'train':
                train_loss.append(epoch_loss)
                train_acc.append(epoch_acc)
            else:
                valid_loss.append(epoch_loss)
                valid_acc.append(epoch_acc)
            print('{} Loss: {:.2f} Acc: {:.1f}'.format(phase, epoch_loss, epoch_acc))

            # deep copy the model
            if phase == 'valid' and epoch_acc > best_acc:
                best_idx = epoch
                best_acc = epoch_acc
                best_model_wts = copy.deepcopy(model.state_dict())
                #                 best_model_wts = copy.deepcopy(model.module.state_dict())
                print('==> best model saved - %d / %.1f' % (best_idx, best_acc))

    time_elapsed = time.time() - since
    print('Training complete in {:.0f}m {:.0f}s'.format(time_elapsed // 60, time_elapsed % 60))
    print('Best valid Acc: %d - %.1f' % (best_idx, best_acc))

    # load best model weights
    model.load_state_dict(best_model_wts)
    torch.save(model.state_dict(), 'president_model.pt')
    print('model saved')
    return model, best_idx, best_acc, train_loss, train_acc, valid_loss, valid_acc

def result_graph(best_idx, best_acc, train_loss, train_acc, valid_loss, valid_acc):
    ####### 결과 그래프 그리기
    print('best model : %d - %1.f / %.1f'%(best_idx, valid_acc[best_idx], valid_loss[best_idx]))
    fig, ax1 = plt.subplots()

    ax1.plot(train_acc, 'b-')
    ax1.plot(valid_acc, 'r-')
    plt.plot(best_idx, valid_acc[best_idx], 'ro')
    ax1.set_xlabel('epoch')
    # Make the y-axis label, ticks and tick labels match the line color.
    ax1.set_ylabel('acc', color='k')
    ax1.tick_params('y', colors='k')

    ax2 = ax1.twinx()
    ax2.plot(train_loss, 'g-')
    ax2.plot(valid_loss, 'k-')
    plt.plot(best_idx, valid_loss[best_idx], 'ro')
    ax2.set_ylabel('loss', color='k')
    ax2.tick_params('y', colors='k')

    fig.tight_layout()
    plt.show()

def test_and_visualize_model(model=model, phase='test', num_images=4):
    # phase = 'train', 'valid', 'test'

    was_training = model.training
    model.eval()
    fig = plt.figure()

    running_loss, running_corrects, num_cnt = 0.0, 0, 0

    with torch.no_grad():
        for i, (inputs, labels) in enumerate(dataloaders[phase]):
            inputs = inputs.to(device)
            labels = labels.to(device)

            outputs = model(inputs)
            _, preds = torch.max(outputs, 1)
            loss = criterion(outputs, labels)  # batch의 평균 loss 출력

            running_loss += loss.item() * inputs.size(0)
            running_corrects += torch.sum(preds == labels.data)
            num_cnt += inputs.size(0)  # batch size

        #         if i == 2: break

        test_loss = running_loss / num_cnt
        test_acc = running_corrects.double() / num_cnt
        print('test done : loss/acc : %.2f / %.1f' % (test_loss, test_acc * 100))

    # 예시 그림 plot
    with torch.no_grad():
        for i, (inputs, labels) in enumerate(dataloaders[phase]):
            inputs = inputs.to(device)
            labels = labels.to(device)

            outputs = model(inputs)
            _, preds = torch.max(outputs, 1)

            # 예시 그림 plot
            for j in range(1, num_images + 1):
                ax = plt.subplot(num_images // 2, 2, j)
                ax.axis('off')
                ax.set_title('%s : %s -> %s' % (
                    'True' if class_names[str(labels[j].cpu().numpy())] == class_names[
                        str(preds[j].cpu().numpy())] else 'False',
                    class_names[str(labels[j].cpu().numpy())], class_names[str(preds[j].cpu().numpy())]))
                imshow(inputs.cpu().data[j])
                plt.pause(1)
            if i == 0: break

    model.train(mode=was_training);  # 다시 train모드로

# train
# model, best_idx, best_acc, train_loss, train_acc, valid_loss, valid_acc = train_model(model, criterion,optimizer_ft,exp_lr_scheduler,num_epochs=300)
## TEST!
# load best model weights
# model = EfficientNet.from_pretrained('efficientnet-b0', weights_path='president_model.pt', num_classes=10).to(device)
checkpoint = torch.load('president_model.pt', map_location=device)
model.load_state_dict(checkpoint)
model.to(device)
test_and_visualize_model(model, phase='valid')
```
