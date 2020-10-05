---
title: "Imitation from Observation Setup"
categories:
  - Installment
tags:
  - Miniconda
  - Imitation
link: https://github.com
---

This theme supports **link posts**, made famous by John Gruber. To use, just add `link: http://url-you-want-linked` to the post's YAML front matter and you're done.

> And this is how a quote looks.

Some [link](#) can also be shown.

1. Install Miniconda in silent mode
https://docs.anaconda.com/anaconda/install/silent-mode/

conda cheat sheet:
https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf
https://interrupt.memfault.com/blog/conda-developer-environments

2. edit bashrc
vim ~/.bashrc
export PATH=~/miniconda/bin:$PATH
source ~/.bashrc

3. rllab 환경 세팅
conda init bash
터미널 한번 껐다가 킨다.
conda create -n rllab3 python=3.5.2 --channel conda-forge

4. 나머지는 sh 파일 만들어서 설치한다.
conda install -y -c anaconda numpy==1.12.1 scipy path.py python-dateutil mako ipywidgets flask h5py pandas scikit-learn
conda install -y -c numba numba
conda install -y -c cogsci pygame
conda install -y -c kne pybox2d
conda install -y -c menpo opencv3=3.1.0
conda install -y pytorch==1.0.0 torchvision==0.2.1 cuda100 -c pytorch
conda install -y mkl-service
<전제: cuda 10.x가 깔려있다>

5. pip package 설치 전 확인
which python && python --version
echo $PATH
which pip 해서 /home/hskim/miniconda/envs/rllab3/bin/pip 나오면 다행. 아니면 specify 해줘서 pip package 설치하자. 안전하게 specify 도 괜찮고.

6. pip package 설치 (requirements.txt) 순서에 따라 깔렸던게 지워질 수도 있다. 그럴경우 추가로 깔아주기.
Pillow
atari-py
ipdb
boto3
PyOpenGL
nose2
pyzmq
tqdm
msgpack-python
line_profiler
redis
pyglet
prettytensor
jupyter
progressbar2
nibabel==2.1.0
pylru==1.0.9
hyperopt
mujoco-py==0.5.7
pip install -r https://raw.githubusercontent.com/Lasagne/Lasagne/master/requirements.txt
https://github.com/Lasagne/Lasagne/archive/master.zip
plotly
tensorflow-gpu==1.15
gym==0.7.4
matplotlib
mpi4py
Cython==0.22
chainer
cloudpickle
keras==1.2.1
polling
joblib==0.10.3
numpy-stl==2.2.0
cached_property
pyprind
imageio

<중간에 chainer 버전 때문에 nvcc 안되면 안된다길래 nvidia-cuda-toolkit 까는거 시도했다가 broken pipe 오류때문에 실패 -> 딱히 필수 아니래서 그냥 냅둠>
sudo apt-get autoremove
sudo apt-get --purge remove
sudo apt-get autoclean
sudo apt-get clean
이렇게 청소한거 같긴한데 잘 모르겠음.

7. aws를 쓸거면
awscli 도 깔자. 안쓰면 aws 관련 config 없애고 stub 도 없애도 되는듯. mode=mujoco-ec2 이것도 없애면 된다.

8. conda 환경 밖의 python package 안쓰는 법
참조: https://stackoverflow.com/questions/17386880/does-anaconda-create-a-separate-pythonpath-variable-for-each-new-environment
unset PYTHONPATH 
conda activate (env_name)

9. python path 설정
참조: https://www.devdungeon.com/content/python-import-syspath-and-pythonpath-tutorial

export PYTHONPATH='/some/extra/path'
python -c "import sys; print(sys.path)"
# Example output
['', '/some/extra/path', '/usr/lib/python2.7', '/usr/lib/python2.7/plat-x86_64-linux-gnu', '/usr/lib/python2.7/lib-tk', '/usr/lib/python2.7/lib-old', '/usr/lib/python2.7/lib-dynload', '/usr/local/lib/python2.7/dist-packages', '/usr/lib/python2.7/dist-packages']

10. tf.compat.v1 으로 바꿔줘야한다는 것들 다 바꿔주기.
imitation_from_observation/rllab/sampler/base.py:116: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

/imitation_from_observation/nets/inception_utils.py:54: The name tf.GraphKeys is deprecated. Please use tf.compat.v1.GraphKeys instead.

imitation_from_observation/nets/inception_v3.py:475: The name tf.variable_scope is deprecated. Please use tf.compat.v1.variable_scope instead.

imitation_from_observation/gym/envs/mujoco/arm_shaping.py:25: The name tf.get_variable is deprecated. Please use tf.compat.v1.get_variable instead.

imitation_from_observation/rllab/sampler/base.py:139: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.

/imitation_from_observation/rllab/sampler/base.py:141: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

imitation_from_observation/rllab/sampler/base.py:144: The name tf.train.Saver is deprecated. Please use tf.compat.v1.train.Saver instead.


11. user 변경 
su cylee
<cuda ld library를 어떻게 연결할까>

2020-10-06 02:08:07.163859: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2020-10-06 02:08:07.187969: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 3499805000 Hz
2020-10-06 02:08:07.188828: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0xac090e0 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2020-10-06 02:08:07.188874: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
2020-10-06 02:08:07.192203: I tensorflow/stream_executor/platform/default/dso_loader.cc:44] Successfully opened dynamic library libcuda.so.1
2020-10-06 02:08:07.306350: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0xacf9c20 initialized for platform CUDA (this does not guarantee that XLA will be used). Devices:
2020-10-06 02:08:07.306404: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): GeForce RTX 2080 Ti, Compute Capability 7.5
2020-10-06 02:08:07.307411: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1618] Found device 0 with properties:
name: GeForce RTX 2080 Ti major: 7 minor: 5 memoryClockRate(GHz): 1.545
pciBusID: 0000:02:00.0


2020-10-06 02:08:07.307603: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcudart.so.10.0'; dlerror: libcudart.so.10.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/hskim/catkin_ws/devel/lib:/opt/ros/kinetic/lib:/opt/ros/kinetic/lib/x86_64-linux-gnu
2020-10-06 02:08:07.307704: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcublas.so.10.0'; dlerror: libcublas.so.10.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/hskim/catkin_ws/devel/lib:/opt/ros/kinetic/lib:/opt/ros/kinetic/lib/x86_64-linux-gnu
2020-10-06 02:08:07.307796: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcufft.so.10.0'; dlerror: libcufft.so.10.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/hskim/catkin_ws/devel/lib:/opt/ros/kinetic/lib:/opt/ros/kinetic/lib/x86_64-linux-gnu
2020-10-06 02:08:07.307897: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcurand.so.10.0'; dlerror: libcurand.so.10.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/hskim/catkin_ws/devel/lib:/opt/ros/kinetic/lib:/opt/ros/kinetic/lib/x86_64-linux-gnu
2020-10-06 02:08:07.307994: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcusolver.so.10.0'; dlerror: libcusolver.so.10.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/hskim/catkin_ws/devel/lib:/opt/ros/kinetic/lib:/opt/ros/kinetic/lib/x86_64-linux-gnu
2020-10-06 02:08:07.308086: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcusparse.so.10.0'; dlerror: libcusparse.so.10.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/hskim/catkin_ws/devel/lib:/opt/ros/kinetic/lib:/opt/ros/kinetic/lib/x86_64-linux-gnu
2020-10-06 02:08:07.341717: I tensorflow/stream_executor/platform/default/dso_loader.cc:44] Successfully opened dynamic library libcudnn.so.7
2020-10-06 02:08:07.341739: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1641] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2020-10-06 02:08:07.341759: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1159] Device interconnect StreamExecutor with strength 1 edge matrix:
2020-10-06 02:08:07.341769: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1165]      0
2020-10-06 02:08:07.341776: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1178] 0:   N


Traceback (most recent call last):
  File "run_trpo_strike.py", line 155, in <module>
    **copyparams
  File "/home/hskim/imitation_from_observation/rllab/algos/trpo.py", line 20, in __init__
    super(TRPO, self).__init__(optimizer=optimizer, **kwargs)
  File "/home/hskim/imitation_from_observation/rllab/algos/npo.py", line 30, in __init__
    super(NPO, self).__init__(**kwargs)
  File "/home/hskim/imitation_from_observation/rllab/algos/batch_polopt.py", line 107, in __init__
    self.sampler = sampler_cls(self, **sampler_args)
  File "/home/hskim/imitation_from_observation/rllab/algos/batch_polopt.py", line 15, in __init__
    super(BatchSampler, self).__init__(algo)
  File "/home/hskim/imitation_from_observation/rllab/sampler/base.py", line 56, in __init__
    self.initialize()
  File "/home/hskim/imitation_from_observation/rllab/sampler/base.py", line 145, in initialize
    saver.restore(sess, self.algo._kwargs['modelname'])
  File "/home/hskim/miniconda/envs/rllab3/lib/python3.5/site-packages/tensorflow_core/python/training/saver.py", line 1280, in restore
    if not checkpoint_management.checkpoint_exists_internal(checkpoint_prefix):
  File "/home/hskim/miniconda/envs/rllab3/lib/python3.5/site-packages/tensorflow_core/python/training/checkpoint_management.py", line 366, in checkpoint_exists_internal
    if file_io.get_matching_files(pathname):
  File "/home/hskim/miniconda/envs/rllab3/lib/python3.5/site-packages/tensorflow_core/python/lib/io/file_io.py", line 363, in get_matching_files
    return get_matching_files_v2(filename)
  File "/home/hskim/miniconda/envs/rllab3/lib/python3.5/site-packages/tensorflow_core/python/lib/io/file_io.py", line 384, in get_matching_files_v2
    compat.as_bytes(pattern))
tensorflow.python.framework.errors_impl.NotFoundError: model; No such file or directory


12. tmux 연결
https://m.blog.naver.com/kimmingul/221339305735



