FROM jupyter/pyspark-notebook:latest
MAINTAINER Mihai Paraschiv <mihai.paraschiv@gmail.com>

USER root

# RSpark config
ENV R_LIBS_USER $SPARK_HOME/R/lib

# libraries needed for R and rpy2
# x11 is needed for plotting in r
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    gfortran \
    gcc \
    libreadline-gplv2-dev \
    x11vnc \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_USER

RUN conda update --all --quiet --yes

RUN conda config --add channels r && \
    conda install --quiet --yes \
    'r-base=3.2*' \
    'r-essentials=1*' \
    && conda clean -tipsy

RUN R --vanilla -e "\
    install.packages(c('forecast', 'lubridate'), \
    repos='http://cran.us.r-project.org', \
    lib='${CONDA_DIR}/lib/R/library')"

RUN conda install --quiet --yes \
    'seaborn' && conda clean -tipsy

RUN pip install 'rpy2==2.8.*'