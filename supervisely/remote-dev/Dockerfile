ARG IMAGE
FROM $IMAGE


#RUN wget https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh
#
#
#RUN bash Anaconda3-2021.05-Linux-x86_64.sh -b -p /miniconda
#ENV PATH=$PATH:c:/miniconda/bin

#RUN conda --version


#RUN conda create -n transt python=3.8
#SHELL ["conda", "run", "-n", "transt", "/bin/bash", "-c"]

# Install PyTorch
RUN pip install torch==1.7.0+cu110 torchvision==0.8.1+cu110 torchaudio==0.7.0 -f https://download.pytorch.org/whl/torch_stable.html
# Install other packages

RUN apt-get install libturbojpeg

RUN git clone https://github.com/supervisely-research/trans-t.git -b develop
RUN pip install -r /trans-t/requirements.txt

RUN pip install supervisely
#RUN conda install matplotlib pandas tqdm
#RUN pip install opencv-python tb-nightly visdom scikit-image tikzplotlib gdown
#RUN conda install cython scipy
#RUN pip install pycocotools jpeg4py
#RUN pip install wget yacs
#RUN pip install shapely==1.6.4.post2


#RUN conda init


RUN apt-get update && apt-get install -y openssh-server
EXPOSE 22

RUN apt-get install -y sudo
RUN mkdir -p /run/sshd



# MORE SECURE: use a trusted RSA key
ARG home=/root
RUN mkdir $home/.ssh
COPY authorized_keys $home/.ssh/authorized_keys
RUN chown root:root $home/.ssh/authorized_keys && \
    chmod 600 $home/.ssh/authorized_keys

COPY sshd_deamon.sh /sshd_deamon.sh
RUN chmod 755 /sshd_deamon.sh
CMD ["/sshd_deamon.sh"]
ENTRYPOINT ["sh", "-c", "/sshd_deamon.sh"]
