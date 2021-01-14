# Exercise 1

## Run Pane

```
docker run -it --name exercise1 ubuntu:21.04 /bin/bash       
[rosulliv@cgifederal.com@op2-mom-ldev325 practical-docker]$ docker run -it --name exercise1 ubuntu:21.04 /bin/bash
root@d3392dbed9f9:/# apt-get install jq
Reading package lists... Done                                                                                                           
Building dependency tree                                            
Reading state information... Done                                   
E: Unable to locate package jq                                                                                                          
root@d3392dbed9f9:/# apt-get update                                                                                                     
Get:1 http://security.ubuntu.com/ubuntu hirsute-security InRelease [90.7 kB]                                                            
Get:2 http://archive.ubuntu.com/ubuntu hirsute InRelease [269 kB]                                                                       
Get:3 http://archive.ubuntu.com/ubuntu hirsute-updates InRelease [90.7 kB]                                                              
Get:4 http://archive.ubuntu.com/ubuntu hirsute-backports InRelease [90.7 kB]                                                            
Get:5 http://archive.ubuntu.com/ubuntu hirsute/main amd64 Packages [1795 kB]                                                            
Get:6 http://archive.ubuntu.com/ubuntu hirsute/restricted amd64 Packages [110 kB]                                                       
Get:7 http://archive.ubuntu.com/ubuntu hirsute/universe amd64 Packages [16.6 MB]                                                        
Get:8 http://archive.ubuntu.com/ubuntu hirsute/multiverse amd64 Packages [252 kB]                                                       
Fetched 19.3 MB in 3s (6281 kB/s)                                                                                                       
Reading package lists... Done                                                                                                           
root@d3392dbed9f9:/# apt-get install jq                                                                                
root@76b7bc9ae3db:/# jq --version 
jq-1.6

iroot@d3392dbed9f9:/# ping google.com                                
bash: ping: command not found                                       
root@d3392dbed9f9:/# apt-get install ping
Reading package lists... Done
Building dependency tree
Reading state information... Done   
Package ping is a virtual package provided by:        
  inetutils-ping 2:1.9.4-13                                                                                                             
  iputils-ping 3:20200821-2                                                                                                             
You should explicitly select one to install. 

root@d3392dbed9f9:/# apt-get install iputils-ping 
...

#
# THIS IS WHERE WE COMMIT THIS VERSION AS IMAGE ubuntu-with-jq:latest !
#

[rosulliv@cgifederal.com@op2-mom-ldev325 practical-docker]$
[rosulliv@cgifederal.com@op2-mom-ldev325 practical-docker]$ docker run -it --name exercise1b ubuntu-with-jq:latest /bin/bash
root@2c90cab5e458:/# ping google.com
PING google.com (64.233.177.113) 56(84) bytes of data.
64 bytes from yx-in-f113.1e100.net (64.233.177.113): icmp_seq=1 ttl=103 time=16.1 ms
64 bytes from yx-in-f113.1e100.net (64.233.177.113): icmp_seq=2 ttl=103 time=16.4 ms
^C
--- google.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 16.078/16.233/16.388/0.155 ms
root@2c90cab5e458:/# 

```

## Build Pane

```
[rosulliv@cgifederal.com@op2-mom-ldev325 core-commons]$ dps
NAMES               IMAGE                   CREATED              STATUS              PORTS
exercise1           ubuntu:21.04            About a minute ago   Up About a minute
myjenkins           jenkins/jenkins:2.225   15 minutes ago       Up 15 minutes       0.0.0.0:8080->8080/tcp, 50000/tcp
registry            registry                2 months ago         Up 2 days           0.0.0.0:5000->5000/tcp
[rosulliv@cgifederal.com@op2-mom-ldev325 core-commons]$ docker commit exercise1
sha256:272c51bd9a24ae4356bba472796741f83f3216f38d8d6ce32b88b5b7c492a08e 
[rosulliv@cgifederal.com@op2-mom-ldev325 core-commons]$ docker commit exercise1 ubuntu-with-jq 
sha256:04fcd2230db29144c59507edfd1f7ffe7e7402c9bce95834dcb22577edf5c657
[rosulliv@cgifederal.com@op2-mom-ldev325 core-commons]$ docker image ls ubuntu
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu              21.04               de35fa744ddc        7 weeks ago         79.6MB
ubuntu              20.04               f643c72bc252        7 weeks ago         72.9MB
ubuntu              19.10               2f6c85efea61        7 months ago        72.9MB
[rosulliv@cgifederal.com@op2-mom-ldev325 core-commons]$ docker image ls ubuntu-with-jq
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
ubuntu-with-jq      latest              04fcd2230db2        10 seconds ago      113MB

```