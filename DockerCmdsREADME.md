# sinmpleDockerCommands
A simple sinmpleDockerCommands


# Docker Basic Commands

## Check Container Running or Stopped
```bash
docker ps -a
```

## List Images
```bash
docker image ls
```

## Run Using Docker
- Downloads if not present and runs in foreground:
```bash
docker run grafana/grafana
docker run hello-world
```

## Run in Background (Detached)
```bash
docker run -d grafana/grafana
```

## Docker Rename Container
```bash
docker ps -a
docker rename old_name new_name
```

## Run in Background with Name
```bash
docker run -d --name new_name selenium/standalone-firefox
```

## Docker Stop
```bash
docker ps -a
docker stop <container_id>
```

## Docker Start
```bash
docker start <container_id>
```

## Docker Restart
```bash
docker restart <container_id>
docker ps -a
```

## Attach to Running Docker
- Using terminal to interact with container:
```bash
docker ps -a
docker exec -it <container_id> bash
ls
exit
```

## Remove Container
```bash
docker stop <container_id>
docker ps -a
docker rm <container_id>
```

## Remove/Delete Container Forcefully
```bash
docker rm -f <container_id>
```

## Remove/Delete All Running Containers
```bash
docker rm -f $(docker ps -a)
```

## Commit and Create New Image
```bash
docker login
docker commit <container_id> karthik/ubuntu
docker push karthik/ubuntu
```

## Remove Images (Not Containers)
```bash
docker images
docker rmi <image_id>
```

## Port Binding
```bash
docker ps
docker inspect <container_id> # Search -> PortBindings:{}
docker run -d -p <host_port>:<container_port> <image>
docker run -d -p 3000:3000 selenium/standalone-firefox
docker ps # Check ports column
docker inspect <container_id> # Search -> PortBindings:{3000}
```

## Docker Volume
- To have persistent or permanent data:
```bash
docker run -v <Permanent_Storage>:<Container_Storage> <ImageName>
```
- BIND Mount -> Using folder on local filesystem:
```bash
mkdir someFolderForData
pwd
ls
docker inspect image grafana/grafana # search for -> GF_PATHS_DATA="var/lib/grafana"
docker run -v $PWD/someFolderForData:/var/lib/grafana -p 3000:3000 grafana/grafana
```
- If permission issue:
```bash
docker run --user 0 -v $PWD/someFolderForData:/var/lib/grafana -p 3000:3000 grafana/grafana
```
- Verify Volume:
```bash
docker ps
pwd
ls someFolderForData
touch abc.txt
docker exec -it <container_id> sh
cd $HOME
cd /var/lib/grafana # Data should be same
touch cde.txt
exit
docker ps
ls
docker inspect <container_id> # Check Mounts:{}
```
