FROM ubuntu:16.04
MAINTAINER Shun Wang <wangshun@aginome.com>
LABEL authors="wangshun@aginome.com" \
    description="ScaleQC lossy compression tool benchmark"

ADD InstallTools.sh /opt
ENV LD_LIBRARY_PATH /usr/local/lib
RUN apt-get update && apt-get install -y --fix-missing ant libbz2-dev build-essential zlib1g-dev unzip libncurses5-dev curl wget python python-pip python-dev cmake libboost-all-dev perl perl-base libxml2-dev libcurl4-gnutls-dev apt-transport-https default-jre default-jdk less vim libtbb-dev git bzip2 gcc g++ make software-properties-common tzdata
RUN cd /opt && bash InstallTools.sh
RUN cd /usr/local/bin && wget -c https://jijiantuchuang-markdown.oss-cn-shenzhen.aliyuncs.com/20-1-6/sqc && chmod 755 /usr/local/bin/sqc
RUN cpan install Parallel::ForkManager

ADD ./bioconda.install.sh /opt
RUN cd /opt && bash ./bioconda.install.sh
ENV PATH $PATH:/opt/miniconda2/bin
ADD ./bioconda.env.yml /opt
RUN cd /opt && conda env create -f ./bioconda.env.yml && conda clean -a
ENV PATH /opt/miniconda2/envs/compressioncompare/bin:$PATH
RUN cd /usr/local/bin && \
    wget -c https://github.com/refresh-bio/DSRC/releases/download/v2.0.2/dsrc-linux-x64-static.tar.gz && \
    tar zxf dsrc-linux-x64-static.tar.gz && mv ./bin/dsrc . && \
    rm -rf ./bin && rm -f dsrc-linux-x64-static.tar.gz && chmod 755 ./dsrc

