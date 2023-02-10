# Elasticstack - docker deployment 




Before running docker-compose, make sure to execute the following command:

~~~bash
sysctl -w vm.max_map_count=262144
~~~


### Windows and docker desktop


#### requirements 
 - requires: WSL 2
 - use a static IP address 

#### Procedure - elastic stack 

1. Install docker desktop 
2. install docker-compose [Other install scearios](https://docs.docker.com/compose/install/other/#on-windows-server)
3. copy docker-compose.yaml and .env to a separate folder 
4. configure vm.max_map_count variable for docker wsl distribution 
    ~~~powershell
    c:\progs\docker\elastic>wsl -l
    Windows Subsystem for Linux Distributions:
    Ubuntu (Default)
    podman-machine-default
    docker-desktop
    docker-desktop-data
    c:\progs\docker\elastic>wsl -d docker-desktop
    labhost8:/mnt/host/c/progs/docker/elastic# sysctl -w vm.max_map_count=262144
    vm.max_map_count = 262144   
    ~~~                         

5. run docker-compose up -d 

