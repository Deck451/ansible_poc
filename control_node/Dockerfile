FROM fedora:latest

RUN dnf update -y && \
    dnf install -y ansible && \
    dnf install -y openssh-clients && \
    dnf clean all

RUN useradd -ms /bin/bash ansible

RUN mkdir -p /home/ansible/.ssh && \
    chown ansible:ansible /home/ansible/.ssh && \
    chmod 700 /home/ansible/.ssh
