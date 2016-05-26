FROM continuumio/anaconda3:latest
MAINTAINER Mihai Paraschiv <mihai.paraschiv@gmail.com>

RUN conda create -y -n py35 python=3.5 anaconda

RUN conda install -y -n py35 seaborn

RUN conda install -y -n py35 -c r r-essentials

# We need to compile rpy2 to be used with Anaconda. We first compile R with
# shared libraries. Afterwards, we compile rpy2.

# compile libraries are needed for rpy2
# x11 is needed for plotting in r
RUN apt-get update --fix-missing && apt-get install -y \
    gcc gfortran g++ build-essential libreadline-gplv2-dev x11vnc && \
    apt-get clean

ENV CONDA_ACTIVATE "source activate py35"
RUN /bin/bash -c "${CONDA_ACTIVATE} && pip install rpy2"

# ENV STARTSCRIPT /opt/start
# RUN echo "#!/bin/bash" > $STARTSCRIPT
# RUN echo "${CONDA_ACTIVATE}" >> $STARTSCRIPT
# RUN chmod +x $STARTSCRIPT

WORKDIR /work