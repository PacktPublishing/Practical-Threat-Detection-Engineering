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

#### configure fleet (optional)
1. Log into kibana, go to management -> fleet 
2. for the server host, enter https://[IP of current machine]:8220
3. wait for the server policy to get generated. 
4. click "Windows" for step 2, and copy the generated PS code block. You will need to make a couple edits, specifically
  - change the --fleet-server-es url. Replace 'http' with 'https'. Additionally, if it uses the server name 'localhost' replace that with the IP address of the local machine.
  -  add the argument --fleet-server-es-insecure
5. Once the installation completes, you will see a fleet server in "Agents" tab under "Fleet"


#### configure fleet outputs 
1. Log into kibana, go to fleet settings 
2. under "outputs" ensure "https://[ip address]:9200" is listed

#### install additional agents
