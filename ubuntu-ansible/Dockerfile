FROM ubuntu:latest

RUN apt update && apt install curl git gpg vim openssh-server sudo -y
RUN apt install python3-venv python3-pip -y
RUN useradd -rm -d /home/ubuntu -s /bin/bash -g root -G sudo -u 1000 ubuntu
RUN echo 'ubuntu:ubuntu' | chpasswd
RUN mkdir /root/.ssh
COPY id_rsa.pub /root/.ssh/authorized_keys
COPY id_rsa /root/.ssh/id_rsa
RUN service ssh start
EXPOSE 22

CMD ["/usr/sbin/sshd","-D"]
