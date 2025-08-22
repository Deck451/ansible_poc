FROM python:3.13-slim

RUN apt-get update && \
    apt-get install -y openssh-server && \
    apt-get install -y sudo && \
    rm -rf /var/lib/apt/lists/*

RUN useradd -ms /bin/bash ansible

RUN mkdir -p /home/ansible/.ssh && \
    chown ansible:ansible /home/ansible/.ssh && \
    chmod 700 /home/ansible/.ssh

ARG ROOT_PASSWORD

RUN echo "root:${ROOT_PASSWORD}" | chpasswd

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
