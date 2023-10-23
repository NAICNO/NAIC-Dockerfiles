FROM ubuntu:16.04
ENV DEBIAN_FRONTEND noninteractive

WORKDIR /tmp

### Install required packages

RUN apt-get clean all &&\
    apt-get update && \
    apt-get install -y \
        zlib1g-dev \
        build-essential \
        curl \
        libncurses5-dev \
        git && \
    apt-get clean && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*


### Install bwa

ENV VERSION 0.7.17
ENV NAME bwa
ENV URL "https://github.com/lh3/bwa/archive/refs/tags/v${VERSION}.tar.gz"

RUN curl -SL $URL | tar -zxv && \
    cd ${NAME}-${VERSION} && \
    make -j 4 && \
    cd .. && \
    cp ./${NAME}-${VERSION}/${NAME} /usr/local/bin/ && \
    strip /usr/local/bin/${NAME}; true && \
    rm -rf ./${NAME}-${VERSION}/


### Installing samtools/htslib/tabix/bgzip

ENV HTSLIB htslib
ENV HTSLIBV 1.18
ENV HTSLIBSHA1 "d8ca374b1977601246ce4a20370c7b78441a01aa"

ENV SAMTOOLS "samtools"
ENV SAMTOOLSV 1.18
ENV SAMTOOLSSHA1 "554bb9043a2da9ea5db85095dce21b742ba1fb71"

RUN git clone https://github.com/samtools/htslib.git && \
    cd ${HTSLIB} && \
    git reset --hard ${HTSLIBSHA1} && \
    make -j 4 && \
    cd .. && \
    cp ./${HTSLIB}/tabix /usr/local/bin/ && \
    cp ./${HTSLIB}/bgzip /usr/local/bin/ && \
    cp ./${HTSLIB}/htsfile /usr/local/bin/ && \
    strip /usr/local/bin/tabix; true && \
    strip /usr/local/bin/bgzip; true && \
    strip /usr/local/bin/htsfile; true && \
git clone https://github.com/samtools/samtools.git && \
    cd ${SAMTOOLS} && \
    git reset --hard ${SAMTOOLSSHA1} && \
    make -j 4 && \
    cp ./${SAMTOOLS} /usr/local/bin/ && \
    cd .. && \
    strip /usr/local/bin/${SAMTOOLS}; true && \
    rm -rf ./${HTSLIB}/ && \
    rm -rf ./${SAMTOOLS}
