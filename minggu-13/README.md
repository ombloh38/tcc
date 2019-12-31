# MINGGU 13
# Docker Swarm  
1. Membuat VMs dengan nama Mesin1 dan Mesin2 menggunakan perintah `docker-machine create --driver virtualbox vm1`
<pre>
lukmanPC@GATHOT-KOCO MINGW64 ~/Documents/tcc/minggu-13 (master)
$ docker-machine create --driver virtualbox mesin1
Running pre-create checks...
Creating machine...
(mesin1) Copying C:\Users\lukmanPC\.docker\machine\cache\boot2docker.iso to C:\U
sers\lukmanPC\.docker\machine\machines\mesin1\boot2docker.iso...
(mesin1) Creating VirtualBox VM...
(mesin1) Creating SSH key...
(mesin1) Starting the VM...
(mesin1) Check network to re-create if needed...
(mesin1) Windows might ask for the permission to configure a dhcp server. Someti
mes, such confirmation window is minimized in the taskbar.
(mesin1) Waiting for an IP...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with boot2docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this vi
rtual machine, run: C:\Program Files\Docker Toolbox\docker-machine.exe env mesin
1

lukmanPC@GATHOT-KOCO MINGW64 ~/Documents/tcc/minggu-13 (master)
$ docker-machine create --driver virtualbox mesin2
Running pre-create checks...
Creating machine...
(mesin2) Copying C:\Users\lukmanPC\.docker\machine\cache\boot2docker.iso to C:\U
sers\lukmanPC\.docker\machine\machines\mesin2\boot2docker.iso...
(mesin2) Creating VirtualBox VM...
(mesin2) Creating SSH key...
(mesin2) Starting the VM...
(mesin2) Check network to re-create if needed...
(mesin2) Windows might ask for the permission to configure a dhcp server. Someti
mes, such confirmation window is minimized in the taskbar.
(mesin2) Waiting for an IP...
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with boot2docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this vi
rtual machine, run: C:\Program Files\Docker Toolbox\docker-machine.exe env mesin
2

lukmanPC@GATHOT-KOCO MINGW64 ~/Documents/tcc/minggu-13 (master)
$
</pre>  
2. Perintahkan mesin1 menjadi swarm manager dengan ssh ke mesin mesin1 kemudian menjalankan perintah `docker swarm init --advertise-addr 192.168.99.101`, IP disini menggunakan ip mesin1. sebelum menjalankan perintah di atas jalankan perintah `docker-machine ssh mesin1`
<pre>
lukmanPC@GATHOT-KOCO MINGW64 ~/Documents/tcc/minggu-13 (master)
$ docker-machine ssh mesin1
   ( '>')
  /) TC (\   Core is distributed with ABSOLUTELY NO WARRANTY.
 (/-_--_-\)           www.tinycorelinux.net

docker@mesin1:~$ docker swarm init --advertise-addr 192.168.99.101
Swarm initialized: current node (6r0evh46xmptdn0vuxr4utrnn) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-1wf4nnd2h1avas2c9wyoplkesnlhcdyq5lattcro5
kf11cwca0-9azwbe8ceh8nhjunlmxl9j0cs 192.168.99.101:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow
 the instructions.
</pre>  
3.  Cek status swarm dengan perintah `docker info`  
<pre>  
docker@mesin1:~$ docker info
Client:
 Debug Mode: false

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 19.03.5
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk
yslog
 Swarm: active
  NodeID: 6r0evh46xmptdn0vuxr4utrnn
  Is Manager: true
  ClusterID: xfhjx3j73u0vhenov7veh5f5r
  Managers: 1
  Nodes: 1
  Default Address Pool: 10.0.0.0/8
  SubnetSize: 24
  Data Path Port: 4789
  Orchestration:
   Task History Retention Limit: 5
  Raft:
   Snapshot Interval: 10000
   Number of Old Snapshots to Retain: 0
   Heartbeat Tick: 1
   Election Tick: 10
  Dispatcher:
   Heartbeat Period: 5 seconds
  CA Configuration:
   Expiry Duration: 3 months
   Force Rotate: 0
  Autolock Managers: false
  Root Rotation In Progress: false
  Node Address: 192.168.99.101
  Manager Addresses:
   192.168.99.101:2377
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: b34a5c8af56e510852c35414db4c1f4fa6172339
 runc version: 3e425f80a8c931f88e6d94a8c831b9d5aa481657
 init version: fec3683
 Security Options:
  seccomp
   Profile: default
 Kernel Version: 4.14.154-boot2docker
 Operating System: Boot2Docker 19.03.5 (TCL 10.1)
 OSType: linux
 Architecture: x86_64
 CPUs: 1
 Total Memory: 989.5MiB
 Name: mesin1
 ID: FWZQ:MEUF:UBAT:XVYR:GKHM:DDV7:AZRP:CY5Q:LLYA:MOCA:36NI:VA5N
 Docker Root Dir: /mnt/sda1/var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
  provider=virtualbox
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine
</pre>  
- Swarm sudah aktif `Swarm: active`  
4. Cek node yang sedang berjalan `docker node ls`   
<pre>
docker@mesin1:~$ docker node ls
ID                            HOSTNAME            STATUS              AVAILABILI
TY        MANAGER STATUS      ENGINE VERSION
6r0evh46xmptdn0vuxr4utrnn *   mesin1              Ready               Active
          Leader              19.03.5
</pre>   
5. Gunakan perintah exit untuk keluar dari mesin1 `exit`
<pre>
docker@mesin1:~$ exit
logout
</pre>  
