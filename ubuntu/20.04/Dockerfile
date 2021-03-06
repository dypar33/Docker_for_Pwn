FROM ubuntu:20.04
LABEL maintainer="dypar33@gmail.com"
WORKDIR /root

RUN apt-get update

# setting timezone
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul 
RUN apt-get install -y tzdata

# setting environment

## To execute 32bit binary
RUN dpkg --add-architecture i386
RUN apt-get update
RUN apt-get install -y libc6-i386 libc6-dev-i386

## To execute arm arch binary
RUN apt-get install -y  gcc-arm-linux-gnueabi g++-arm-linux-gnueabi gcc-aarch64-linux-gnu g++-aarch64-linux-gnu gdb-multiarch qemu-user-static
RUN cp /usr/arm-linux-gnueabi/lib/ld-linux.so.3 /lib
RUN cp /usr/arm-linux-gnueabi/lib/libc.so.6 /lib
RUN cp /usr/arm-linux-gnueabi/lib/libgcc_s.so.1 /lib
RUN cp /usr/aarch64-linux-gnu/lib/ld-linux-aarch64.so.1 /lib
# RUN cp /usr/aarch64-linux-gnu/lib/libc.so.6  /lib  --> arm 32bit libc.so.6과 충돌이 나기 때문에 환경 변수 설정을 따로하거나 libc를 바꿔가면서 실행해야할 것 같다. 

## Utils
RUN apt-get install -y net-tools netcat curl wget git
RUN apt-get install -y vim file 
RUN apt-get install -y gcc gdb 

## Ruby
RUN apt-get -y install ruby

## Python
RUN apt-get install -y python2 python2-dev
RUN apt-get install -y python3 python3-dev python3-pip

RUN curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py
RUN python2 get-pip.py
RUN rm -rf get-pip.py

RUN python2 -m pip install --upgrade pip setuptools
RUN python3 -m pip install --upgrade pip setuptools

## Tools for Pwn
RUN python2 -m pip install --upgrade pwntools ropgadget 
RUN python3 -m pip install --upgrade pwntools pycrypto pycryptodome gmpy2

RUN gem install one_gadget

RUN apt-get install -y binwalk

RUN git clone https://github.com/longld/peda.git ~/peda
RUN echo "source ~/peda/peda.py" >> ~/.gdbinit
RUN git clone https://github.com/scwuaptx/Pwngdb.git
RUN cp ~/Pwngdb/.gdbinit ~/

RUN git clone https://github.com/zweisamkeit/RSHack.git
RUN ln -s /root/RSHack/rshack.py /usr/bin/rshack

RUN mkdir workspace
WORKDIR /root/workspace/
CMD ["/bin/bash"]
