FROM nvidia/cuda:10.0-devel 
# install Anaconda3-5.2.0 for python3.6
RUN apt-get update \
	&& apt-get install wget -y \
	&& wget https://repo.continuum.io/archive/Anaconda3-5.2.0-Linux-x86_64.sh \
	&& /bin/bash Anaconda3-5.2.0-Linux-x86_64.sh -b -p /opt/conda \
	&& apt-get remove wget --purge -y \
	&& apt-get autoremove -y \
	&& apt-get autoclean -y \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf Anaconda3-5.2.0-Linux-x86_64.sh
ENV PATH /opt/conda/bin:$PATH

# install tensorflow-gpu=1.12
RUN conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ \
	&& conda install tensorflow-gpu=1.12 -y

# install opencv lib for image processing
RUN pip install msgpack opencv-python \
	&& apt-get update \
	&& apt-get install libsm6 libxrender1 libxext-dev -y \
	&& apt-get autoremove -y \
	&& apt-get autoclean -y \
	&& rm -rf /var/lib/apt/lists/*

# install google object detection
RUN apt-get update \
	&& apt-get install git -y \
	&& git clone https://gitee.com/study-cooperation/models.git \
	&& /bin/bash models/research/setup.sh \
	&& mkdir /opt/object_detection \
	&& cp -r models/research/build/lib/* /opt/object_detection \
	&& apt-get remove git --purge -y \
	&& apt-get autoremove -y \
	&& apt-get autoclean -y \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /models
ENV PYTHONPATH /opt/object_detection:$PYTHONPATH

CMD ["/bin/bash"]
