FROM python:3.13-slim

RUN apt-get update && \
    apt-get install -y openssh-server && \
    apt-get install -y sudo && \
    rm -rf /var/lib/apt/lists/*

RUN useradd -ms /bin/bash ansible

RUN mkdir -p /home/ansible/.ssh && \
    chown ansible:ansible /home/ansible/.ssh && \
    chmod 700 /home/ansible/.ssh && \
    usermod -aG sudo ansible

ARG SSH_USER_PASSWORD

RUN echo "ansible:${SSH_USER_PASSWORD}" | chpasswd

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
