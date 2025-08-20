# ansible_poc

A proof-of-concept project demonstrating running an ansible playbook on 3 backend servers,
running under a Docker container using Docker Compose.

## Quick Start

### clone the repository and cd into it
```sh
git clone https://github.com/deck451/ansible_poc.git
cd ./ansible_poc
```

### generate ssh keys (and set permissions for them) for the control node and servers
```sh
ssh-keygen -t ed25519 -f ./control_node/ansible_key -N ""
sudo chmod 600 ./control_node/ansible_key.pub
sudo chmod 600 ./control_node/ansible_key
```

### start the containers
```sh
docker compose up --build
```

### docker exec into the control node
```sh
docker exec -it control_node /bin/bash
```

### ssh into any of the servers from the control node
```sh
ssh server_0 -l ansible
```