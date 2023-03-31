FROM ubuntu:latest

RUN apt-get update && apt install git gpg vim openssh-server unzip sudo -y
RUN apt-get install python3-venv python3-pip -y
# Install networking tools
RUN apt-get install iputils-ping curl dnsutils nmap tcpdump netcat iproute2 net-tools -y
RUN apt-get traceroute links -y
# Install speedtest
RUN curl -s https://packagecloud.io/install/repositories/ookla/speedtest-cli/script.deb.sh | sudo bash
RUN apt-get install speedtest -y

RUN useradd -rm -d /home/ubuntu -s /bin/bash -g root -G sudo -u 1000 ubuntu
RUN echo 'ubuntu:ubuntu' | chpasswd
RUN mkdir /root/.ssh
COPY id_rsa.pub /root/.ssh/authorized_keys
COPY id_rsa /root/.ssh/id_rsa
RUN service ssh start

# Install DNS Leak test
COPY dnsleaktest.sh /root/dnsleaktest.sh
RUN chmod +x /root/dnsleaktest.sh

RUN mkdir /opt/script-server
WORKDIR /opt/script-server
RUN wget https://github.com/bugy/script-server/releases/latest/download/script-server.zip
RUN unzip script-server.zip
RUN rm script-server.zip
RUN pip install -r requirements.txt
COPY conf.json /opt/script-server/conf/conf.json
COPY startup.sh /opt/script-server/startup.sh
COPY runners/ /opt/script-server/conf/runners/

EXPOSE 22
EXPOSE 5000

CMD ["/bin/bash", "-c", "./startup.sh"]