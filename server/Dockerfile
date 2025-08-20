FROM python:3.13-slim

RUN apt-get update && \
    apt-get install -y openssh-server && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 22

RUN useradd -ms /bin/bash ansible && \
    mkdir -p /home/ansible/.ssh

CMD ["/usr/sbin/sshd", "-D"]
