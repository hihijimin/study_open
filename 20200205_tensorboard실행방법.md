참고  
[1] https://eehoeskrap.tistory.com/322, [TensorFlow] pb 파일 TensorBoard에 띄우기  
  
위 참고 사이트 설명대로 똑같이 적용해봄!

아래 내용과 같이 .py 파일 만들기(예: import_pb_to_tensorboard.py)

    # Copyright 2017 The TensorFlow Authors. All Rights Reserved.
    # Licensed under the Apache License, Version 2.0 (the "License");
    # you may not use this file except in compliance with the License.
    # You may obtain a copy of the License at # # http://www.apache.org/licenses/LICENSE-2.0
    # Unless required by applicable law or agreed to in writing, software
    # distributed under the License is distributed on an "AS IS" BASIS,
    # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    # See the License for the specific language governing permissions and
    # limitations under the License.
    # ================================
    # """Imports a protobuf model as a graph in Tensorboard."""
    
    from __future__ import absolute_import
    from __future__ import division
    from __future__ import print_function
    import argparse
    import sys
    from tensorflow.core.framework import graph_pb2
    from tensorflow.python.client import session
    from tensorflow.python.framework import importer
    from tensorflow.python.framework import ops
    from tensorflow.python.platform import app
    from tensorflow.python.platform import gfile
    from tensorflow.python.summary import summary
    # Try importing TensorRT ops if available
    # TODO(aaroey): ideally we should import everything from contrib, but currently
    # tensorrt module would cause build errors when being imported in
    # tensorflow/contrib/__init__.py. Fix it.
    # pylint: disable=unused-import,g-import-not-at-top,wildcard-import
    try:
        from tensorflow.contrib.tensorrt.ops.gen_trt_engine_op import *
    except ImportError:
        pass
    # pylint: enable=unused-import,g-import-not-at-top,wildcard-import
    def import_to_tensorboard(model_dir, log_dir):
        """View an imported protobuf model (`.pb` file) as a graph in Tensorboard.
        Args:
            model_dir: The location of the protobuf (`pb`) model to visualize
            log_dir: The location for the Tensorboard log to begin visualization from.
        Usage:
            Call this function with your model location and desired log directory.
            Launch Tensorboard by pointing it to the log directory.
            View your imported `.pb` model as a graph. """
        with session.Session(graph=ops.Graph()) as sess:
            with gfile.GFile(model_dir, "rb") as f:
                graph_def = graph_pb2.GraphDef()
                graph_def.ParseFromString(f.read())
                importer.import_graph_def(graph_def)

            pb_visual_writer = summary.FileWriter(log_dir)
            pb_visual_writer.add_graph(sess.graph)
            print("Model Imported. Visualize by running: " "tensorboard --logdir={}".format(log_dir))

    def main(unused_args):
        import_to_tensorboard(FLAGS.model_dir, FLAGS.log_dir)

    if __name__ == "__main__":
        parser = argparse.ArgumentParser()
        parser.register("type", "bool", lambda v: v.lower() == "true")
        parser.add_argument(
            "--model_dir", type=str, default="", required=True,
            help="The location of the protobuf (\'pb\') model to visualize.")
        parser.add_argument(
            "--log_dir", type=str, default="", required=True,
            help="The location for the Tensorboard log to begin visualization from.")
        FLAGS, unparsed = parser.parse_known_args()
        app.run(main=main, argv=[sys.argv[0]] + unparsed)
------------------------------------

그런 후, **$ python import_pb_to_tensorboard.py --model_dir ./save/frozen.pb --log_dir ./** 이라고 작성한다.  
(위 참고설명에 의하면, pb 파일의 path를 model_dir에 지정해주고, log 디렉토리인 tensorboard을 생성하여 log_dir을 설정해주는 거라 한다)  
pycham에서 예시:  
![image](https://user-images.githubusercontent.com/56099627/73831178-39ef0680-4849-11ea-9850-56f23ab1a30d.png)  

    C:\Users\humanict\Anaconda36\envs\ahn\python.exe D:/CRNN-master/CRNN/import_pb_to_tensorboard.py --model_dir ./save/frozen.pb --log_dir ./
    C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\h5py\__init__.py:36: FutureWarning: Conversion of the second argument of issubdtype from `float` to `np.floating` is deprecated. In future, it will be treated as `np.float64 == np.dtype(float).type`.
      from ._conv import register_converters as _register_converters
    2020-02-05 18:40:55.346347: I tensorflow/core/platform/cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX AVX2
    2020-02-05 18:40:55.575241: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1432] Found device 0 with properties: 
    name: GeForce GTX 1070 major: 6 minor: 1 memoryClockRate(GHz): 1.7845
    pciBusID: 0000:01:00.0
    totalMemory: 8.00GiB freeMemory: 6.63GiB
    2020-02-05 18:40:55.575504: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1511] Adding visible gpu devices: 0
    2020-02-05 18:40:55.945493: I tensorflow/core/common_runtime/gpu/gpu_device.cc:982] Device interconnect StreamExecutor with strength 1 edge matrix:
    2020-02-05 18:40:55.945637: I tensorflow/core/common_runtime/gpu/gpu_device.cc:988]      0 
    2020-02-05 18:40:55.945722: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1001] 0:   N 
    2020-02-05 18:40:55.945915: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1115] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 6384 MB memory) -> physical GPU (device: 0, name: GeForce GTX 1070, pci bus id: 0000:01:00.0, compute capability: 6.1)
    Model Imported. Visualize by running: tensorboard --logdir=./

    Process finished with exit code 0
--------------------------------------

명령어를 통해 링크(http://AI-SVN:6006)에 접속하여 pb파일을 tensorboard로 확인 가능하다
명령어: **tensorboard --logdir=./**

    (ahn) D:\CRNN-master\CRNN>tensorboard --logdir=./
    C:\Users\humanict\Anaconda36\envs\ahn\lib\site-packages\h5py\__init__.py:36: FutureWarning: Conversion of the second argument of issubdty
    pe from `float` to `np.floating` is deprecated. In future, it will be treated as `np.float64 == np.dtype(float).type`.
      from ._conv import register_converters as _register_converters
    TensorBoard 1.12.2 at http://AI-SVN:6006 (Press CTRL+C to quit)
--------------------------------------------
