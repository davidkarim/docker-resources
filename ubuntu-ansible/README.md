# Description
This image can be used to test Ansible scripts locally. It launches Ubuntu with ssh server running which I can then connect to locally with my key and also run Ansible on it.

## How to run

```bash
# Run the copy keys shell script
./copy_keys.sh

# Build image
docker image build . -t ubuntu-ansible

# Run container detached, and remove when stopped
docker container run -d --rm --name ansible-test -p 22:22 ubuntu-ansible

# Connect to running container
docker container exec -it ansible-test /bin/bash

# SSH into container
ssh -o "StrictHostKeyChecking=no" root@localhost # uses ssh keys
ssh -o "StrictHostKeyChecking=no" ubuntu@localhost # uses configured password
```

