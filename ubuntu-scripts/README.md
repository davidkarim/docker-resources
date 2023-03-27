# Description
This image runs the script-server application which runs as a web server to run scripts easily. It launches Ubuntu with ssh server running which I can then connect to locally with my key.

## How to run

```bash
# Run the copy keys shell script
./copy_keys.sh

# Build image
docker image build . -t ubuntu-scripts

# Run container detached, and remove when stopped
# Port 5000 is used on Macs for AirPlay
docker container run -d --rm --name scripts-server -p 22:22 -p 8000:5000 ubuntu-scripts

# Connect to running container
docker container exec -it scripts-server /bin/bash

# SSH into container
ssh -o "StrictHostKeyChecking=no" root@localhost # uses ssh keys
ssh -o "StrictHostKeyChecking=no" ubuntu@localhost # uses configured password

# Launch server and connect to it
python3 launcher.py
# Go to: http://localhost:8000/index.html#/
```
## Deployment on Synology
The files were hand copied to Synology under /volume1/homes/dkarim/ubuntu-scripts.

```bash
# Build the image from Synology CLI:
docker image build . -f Dockerfile -t ubuntu-scripts
# Then stop and delete container from Synology Docker client
# and recreate it.
# The mappings used were ports 2223:22 and 8000:5000
# The Synology reverse proxy has ability to add a custom header for web sockets. This
# was necessary to make the wss requests the app does to work.
```