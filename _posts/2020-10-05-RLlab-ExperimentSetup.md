---
title: "Imitation from Observation RLLab Setup"
categories:
  - Installment
tags:
  - Miniconda
  - Imitation
---

# 1. Install Miniconda in silent mode
https://docs.anaconda.com/anaconda/install/silent-mode/

conda cheat sheet:
https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf
https://interrupt.memfault.com/blog/conda-developer-environments

# 2. edit bashrc
vim ~/.bashrc
export PATH=~/miniconda/bin:$PATH
source ~/.bashrc

# 3. rllab 환경 세팅
conda init bash
터미널 한번 껐다가 킨다.
conda create -n rllab3 python=3.5.2 --channel conda-forge

# 4. 나머지는 sh 파일 만들어서 설치한다.
conda install -y -c anaconda numpy==1.12.1 scipy path.py python-dateutil mako ipywidgets flask h5py pandas scikit-learn
conda install -y -c numba numba
conda install -y -c cogsci pygame
conda install -y -c kne pybox2d
conda install -y -c menpo opencv3=3.1.0
conda install -y pytorch==1.0.0 torchvision==0.2.1 cuda100 -c pytorch
conda install -y mkl-service
<전제: cuda 10.x가 깔려있다>

# 5. pip package 설치 전 확인
which python && python --version
echo $PATH
which pip 해서 /home/hskim/miniconda/envs/rllab3/bin/pip 나오면 다행. 아니면 specify 해줘서 pip package 설치하자. 안전하게 specify 도 괜찮고.

# 6. pip package 설치 (requirements.txt) 순서에 따라 깔렸던게 지워질 수도 있다. 그럴경우 추가로 깔아주기.
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
https://askubuntu.com/questions/30993/fixing-software-center-catalog/183625#183625

LD_LIBRARY_PATH: /home/hskim/catkin_ws/devel/lib:/opt/ros/kinetic/lib:/opt/ros/kinetic/lib/x86_64-linux-gnu:/usr/local/cuda/lib64:/usr/lib/x86_64-linux-gnu


# 7. aws를 쓸거면
awscli 도 깔자. 안쓰면 aws 관련 config 없애고 stub 도 없애도 되는듯. mode=mujoco-ec2 이것도 없애면 된다.

# 8. conda 환경 밖의 python package 안쓰는 법
참조: https://stackoverflow.com/questions/17386880/does-anaconda-create-a-separate-pythonpath-variable-for-each-new-environment
unset PYTHONPATH 
conda activate (env_name)

# 9. python path 설정
참조: https://www.devdungeon.com/content/python-import-syspath-and-pythonpath-tutorial

export PYTHONPATH='/some/extra/path'
python -c "import sys; print(sys.path)"
Example output
['', '/some/extra/path', '/usr/lib/python2.7', '/usr/lib/python2.7/plat-x86_64-linux-gnu', '/usr/lib/python2.7/lib-tk', '/usr/lib/python2.7/lib-old', '/usr/lib/python2.7/lib-dynload', '/usr/local/lib/python2.7/dist-packages', '/usr/lib/python2.7/dist-packages']

Tried writing PYTHONPATH at .bashrc but highly error-

# 10. tf.compat.v1 으로 바꿔줘야한다는 것들 다 바꿔주기.
imitation_from_observation/rllab/sampler/base.py:116: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

/imitation_from_observation/nets/inception_utils.py:54: The name tf.GraphKeys is deprecated. Please use tf.compat.v1.GraphKeys instead.

imitation_from_observation/nets/inception_v3.py:475: The name tf.variable_scope is deprecated. Please use tf.compat.v1.variable_scope instead.

imitation_from_observation/gym/envs/mujoco/arm_shaping.py:25: The name tf.get_variable is deprecated. Please use tf.compat.v1.get_variable instead.

imitation_from_observation/rllab/sampler/base.py:139: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.

/imitation_from_observation/rllab/sampler/base.py:141: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

imitation_from_observation/rllab/sampler/base.py:144: The name tf.train.Saver is deprecated. Please use tf.compat.v1.train.Saver instead.


# 11. user 변경 
su cylee
<cuda ld library를 어떻게 연결할까> /usr/...?/cuda/bin whatever
By using ln operation, rename ld library link 
https://linuxize.com/post/how-to-create-symbolic-links-in-linux-using-the-ln-command/


# 12. tmux 연결
https://m.blog.naver.com/kimmingul/221339305735

# 13. Jupyter lab python path setting


# 14. Install VLC player to watch expert mp4 files

# 15. LD library path (cuda 10.0) 바꿔주기
libcufft.so.10.0'; dlerror: libcufft.so.10.0: cannot open shared object file: No such file or directory; 
2020-10-08 17:40:03.166569: W tensorflow/stream_executor/platform/default/dso_loader.cc:55] Could not load dynamic library 'libcurand.so.10.0'; dlerror: libcurand.so.10.0: cannot open shared object file: No such file or directory; 
'libcusolver.so.10.0';
'libcusparse.so.10.0';


