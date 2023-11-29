FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y --no-install-recommends wget \
    build-essential \
    autoconf \
    automake \
    make \
    gcc \
    perl \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-gnutls-dev \
    libssl-dev \
    libncurses5-dev \
    unzip \
    default-jdk \
    python3 \
    python-is-python3 \
    pip \
    fastqc

# fastqc
RUN fastqc --version

# STAR
RUN wget https://github.com/alexdobin/STAR/releases/download/2.7.10b/STAR_2.7.10b.zip
RUN unzip STAR_2.7.10b.zip 
RUN export PATH=$PATH:/STAR_2.7.10b/Linux_x86_64/

# bcftools
RUN wget https://github.com/samtools/bcftools/releases/download/1.18/bcftools-1.18.tar.bz2
RUN tar -xjvf bcftools-1.18.tar.bz2 
RUN cd bcftools-1.18 && make && make install

# samtools
RUN wget https://github.com/samtools/samtools/releases/download/1.16.1/samtools-1.16.1.tar.bz2
RUN tar -xjvf samtools-1.16.1.tar.bz2
RUN cd samtools-1.16.1 && ./configure && make && make install

# picard
RUN wget https://github.com/broadinstitute/picard/releases/download/2.27.5/picard.jar
RUN java --version
# We can pass the arguments to picard separated by spaces
RUN java -jar /picard.jar; exit 0

# bedtools
RUN wget https://github.com/arq5x/bedtools2/releases/download/v2.30.0/bedtools-2.30.0.tar.gz
RUN tar -zxvf bedtools-2.30.0.tar.gz 
RUN cd bedtools2 && make && make install && ./bin/bedtools --version
RUN export PATH=$PATH:/bedtools2/bin

# salmon
RUN apt-get install cmake curl unzip -y
RUN wget https://github.com/COMBINE-lab/salmon/releases/download/v1.9.0/salmon-1.9.0_linux_x86_64.tar.gz
RUN tar zxf salmon-1.9.0_linux_x86_64.tar.gz
RUN cd salmon-1.9.0_linux_x86_64/bin && ./salmon --version
 
# multiqc
RUN pip install multiqc==1.13

# checks
RUN fastqc --version
RUN samtools --version
RUN bedtools --version
RUN bcftools --version
RUN multiqc --version
RUN java -jar /picard.jar; exit 0