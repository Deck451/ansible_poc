FROM fedora:latest

RUN dnf update -y && \
    dnf install -y ansible && \
    dnf install -y openssh-server && \
    dnf install -y openssh-clients && \
    dnf clean all

RUN useradd -ms /bin/bash ansible

RUN mkdir -p /home/ansible/.ssh && \
    chown ansible:ansible /home/ansible/.ssh && \
    chmod 700 /home/ansible/.ssh && \
    usermod -aG wheel ansible

RUN ssh-keygen -A

ARG ANSIBLE_VAULT_PASSWORD
ARG SSH_USER_PASSWORD

RUN echo "\"${ANSIBLE_VAULT_PASSWORD}\"" > /home/ansible/.vault_pass && \
    chown ansible:ansible /home/ansible/.vault_pass && \    
    chmod 600 /home/ansible/.vault_pass && \
    echo "ansible_become_pass: \"${SSH_USER_PASSWORD}\"" > /home/ansible/vault.yml && \
    ansible-vault encrypt /home/ansible/vault.yml --vault-password-file /home/ansible/.vault_pass && \
    chown ansible:ansible /home/ansible/vault.yml && \
    chmod 600 /home/ansible/vault.yml
    
RUN echo "ansible:${SSH_USER_PASSWORD}" | chpasswd

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
