FROM nvidia/cuda:11.1.1-devel-ubuntu18.04

# Install base packages


RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        curl \
        nano \
        unzip \
        ca-certificates\
        libjpeg-dev \
        libpng-dev \
        software-properties-common \
    && apt-get -qq -y autoremove \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /var/log/dpkg.log



RUN add-apt-repository universe
RUN apt-get update

RUN apt-get remove -y python3 python3-pip
RUN apt-get install -y python3.8 python3-pip
RUN update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 1

# Install PyTorch
RUN pip install torch==1.7.0+cu110 torchvision==0.8.1+cu110 torchaudio==0.7.0 -f https://download.pytorch.org/whl/torch_stable.html


# Install trans-t packages

RUN pip install --upgrade pip

RUN apt-get install libturbojpeg


RUN git clone https://github.com/supervisely-ecosystem/trans-t.git
RUN pip install -r /trans-t/requirements.txt

RUN pip install supervisely==6.1.95

RUN mkdir /trans-t/data/model/
RUN cd /trans-t/data/model/ && wget --no-check-certificate 'https://drive.google.com/uc?id=1uxnvaKdTtYj-IgmrYwi2hCD5ZddTK2d8&export=download' -O transt.pth

RUN mv /trans-t/ /root/trans-t/

