define image resize && tensor 형태 변형(onnx  
```
def load_image(path):
    # load image 
    #rawimg1 = cv2.imread(path)
    rawimg = io.imread(path)
#     print(rawimg1.shape, rawimg2.shape)
#     np.savetxt('result_cv2.csv', rawimg1, fmt='%3.7f', newline=',', header='result_pred_cv2')
#     np.savetxt('result_pred_io.csv', rawimg2, fmt='%3.7f', newline=',', header='result_pred_io')
    
    img = np.rollaxis(rawimg, 2, 0) 
    img416416 = resize(img / 255, (3, 416, 416), anti_aliasing=True)
    ximg = img416416[np.newaxis, :, :, :] # np.newaxis 차원 늘려즘
    ximg = ximg.astype(np.float32)
    print(type(rawimg), rawimg.shape, ximg.shape)
    
    ## convert image to imge_tensor
    #images_tensor = torch.tensor(ximg, dtype=torch.float32)
    return ximg, rawimg
```
ver 1
```
#Tensor = torch.cuda.FloatTensor if torch.cuda.is_available() else torch.FloatTensor
Tensor = torch.FloatTensor
rawimg = cv2.imread('sample1.jpg', cv2.IMREAD_COLOR) # (h,w,3)
print(rawimg.shape, type(rawimg))
imgTensor = torchvision.transforms.ToTensor()(rawimg) # (3,h,w)
imgTensor, _ = pad_to_square(imgTensor, 0) # padding : 큰 길이에 맞춰 (3,w,w)
imgTensor = _resize(imgTensor, 416)
imgTensor = imgTensor.unsqueeze(0)
ximg = Variable(imgTensor.type(Tensor))
print(ximg.shape, type(ximg))
```
ver 2
```
rawimg = cv2.imread('sample1.jpg', cv2.IMREAD_COLOR) # (h,w,3)
print(rawimg.shape, type(rawimg))
images_ok, _, _, _ = letterbox(rawimg, 416, (127.5, 127.5, 127.5), 'square') # (416,416,3)
print(images_ok.shape, type(images_ok))
# 416,416 종횡비 맞추기
ximg = torchvision.transforms.Compose([
        torchvision.transforms.ToPILImage(),
        torchvision.transforms.ToTensor(),
])(images_ok)
print(ximg.shape, type(ximg))
ximg = np.expand_dims(ximg,axis=0) # (1,h,w,3)
print(ximg.shape, type(ximg))

#ximg, rawimg = load_image("sample1.jpg")
# load original image
rawimg = Image.open('sample1.jpg').convert('RGB')
rawimg = ImageDraw.Draw(rawimg)
# Extract image as PyTorch tensor
ximg = torchvision.transforms.ToTensor()(Image.open('sample1.jpg').convert('RGB'))
# Pad to square resolution
ximg, _ = pad_to_square(ximg)
# Resize
ximg = resize(ximg, input_shape[-1])
ximg=ximg[np.newaxis, :, :, :] # np.newaxis 차원 늘려즘
```    
ver 3
```    
img = cv2.imread("dog-cycle-car.png")
img = cv2.resize(img, (416,416)) 
img_ =  img[:,:,::-1].transpose((2,0,1))
img_ = img_[np.newaxis,:,:,:]/255.0
img_ = torch.from_numpy(img_).float()
img_ = Variable(img_)
```
