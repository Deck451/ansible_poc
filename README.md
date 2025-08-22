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
The public key will be mounted on the servers as `authorized_keys` file.
It could also have `644` permissions instead of `600`, but `600` is safest.
The general idea is that it should not be group-writable, nor world-writable.

```sh
ssh-keygen -t ed25519 -f ./control_node/ansible_key -N ""
sudo chmod 600 ./control_node/ansible_key.pub
sudo chmod 600 ./control_node/ansible_key
```

### start the containers
```sh
docker compose up --build
```

### docker exec into the control node, as the `ansible` user
```sh
docker exec -it --user ansible control_node /bin/bash
```

### manually `ssh` into any of the servers from the control node
```sh
ssh ansible@server_0
ssh ansible@server_1
ssh ansible@server_2
```

### test ansible `ssh` connection
The `ssh` key should be the default one, so no need to specify it in the command below.
Same goes for the inventory file.
```sh
ansible all -m ping
```