# docker build -t pwnapi .
# docker run --rm -v $PWD:/pwd --cap-add=SYS_PTRACE --security-opt seccomp=unconfined -d --name pwnapi -i pwnapi
# docker exec -it pwnapi /bin/bash

FROM ubuntu:19.10
ENV LC_CTYPE C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive
RUN dpkg --add-architecture i386 && \
apt-get update && \
apt-get install -y build-essential jq strace ltrace curl wget rubygems gcc dnsutils netcat gcc-multilib net-tools vim gdb gdb-multiarch python python3 python3-pip python3-dev libssl-dev libffi-dev wget git make procps libpcre3-dev libdb-dev libxt-dev libxaw7-dev python-pip libc6:i386 libncurses5:i386 libstdc++6:i386 && \
pip install capstone requests r2pipe && \
pip3 install keystone-engine unicorn capstone ropper && \
mkdir tools
WORKDIR /root/tools/
RUN git clone https://github.com/JonathanSalwan/ROPgadget
WORKDIR /root/tools/ROPgadget
RUN python setup.py install
WORKDIR /root/tools/
RUN git clone https://github.com/radare/radare2
WORKDIR /root/tools/radare2
RUN sys/install.sh
WORKDIR /root/tools/
RUN git clone https://github.com/pwndbg/pwndbg
WORKDIR /root/tools/pwndbg/
RUN ./setup.sh && \
gem install one_gadget
WORKDIR /root/
RUN rm .bashrc && git clone https://github.com/TarushS/bashrc
WORKDIR /root/bashrc
RUN mv .bashrc /root
WORKDIR /root/
RUN rm -r bashrc
WORKDIR /root/tools/
RUN git clone https://github.com/TarushS/pwnapi
WORKDIR /root/tools/pwnapi
RUN make install
