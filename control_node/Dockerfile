FROM fedora:latest

ARG SSH_USER_PASSWORD
ARG ANSIBLE_VAULT_PASSWORD

# install required packages
RUN dnf update -y && \
    dnf install -y ansible && \
    dnf install -y openssh-server && \
    dnf install -y openssh-clients && \
    dnf clean all

# add and configure ansible user
RUN useradd -ms /bin/bash ansible && \
    usermod -aG wheel ansible && \
    echo "ansible:${SSH_USER_PASSWORD}" | chpasswd

# configure ssh
RUN mkdir -p /home/ansible/.ssh && \
    chown ansible:ansible /home/ansible/.ssh && \
    chmod 700 /home/ansible/.ssh && \
    ssh-keygen -A

# configure ansible vault and become password
RUN echo "\"${ANSIBLE_VAULT_PASSWORD}\"" > /home/ansible/.vault_pass && \
    chown ansible:ansible /home/ansible/.vault_pass && \    
    chmod 600 /home/ansible/.vault_pass && \
    echo "ansible_become_pass: \"${SSH_USER_PASSWORD}\"" > /home/ansible/vault.yml && \
    ansible-vault encrypt /home/ansible/vault.yml --vault-password-file /home/ansible/.vault_pass && \
    chown ansible:ansible /home/ansible/vault.yml && \
    chmod 600 /home/ansible/vault.yml
    
# port for ssh and start sshd
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
