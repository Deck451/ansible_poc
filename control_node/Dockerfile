FROM fedora:latest

RUN dnf update -y && \
    dnf install -y ansible && \
    dnf install -y openssh-clients && \
    dnf clean all
