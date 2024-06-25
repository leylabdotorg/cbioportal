# cBioPortal cloud deployment using GCP Compute Engine

This guide details the process of deploying cBioPortal to a Compute Engine VM using Docker Compose.

## Compute Engine

Please visit the [cBioPortal Docs](https://docs.cbioportal.org/hardware-requirements/) to view the performance and hardware requirements. A basic GCP VM 
will run the app, but more disk space is required for large datasets. Once you have a VM that adheres to the requirements, SSH into it either from your browser
or by installing the [gcloud CLI](https://cloud.google.com/sdk/docs/install).

## Deployment

### Install Git:

```
$ sudo -s (if necessary)
$ apt-get update
$ apt-get install git -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  git-man liberror-perl patch
Suggested packages:
  git-daemon-run | git-daemon-sysvinit git-doc git-email git-gui gitk gitweb git-cvs git-mediawiki git-svn ed diffutils-doc
The following NEW packages will be installed:
  git git-man liberror-perl patch
0 upgraded, 4 newly installed, 0 to remove and 2 not upgraded.
Need to get 9377 kB of archives.
After this operation, 48.0 MB of additional disk space will be used.
Get:1 file:/etc/apt/mirrors/debian.list Mirrorlist [30 B]
Get:2 https://deb.debian.org/debian bookworm/main amd64 liberror-perl all 0.17029-2 [29.0 kB]
Get:3 https://deb.debian.org/debian bookworm/main amd64 git-man all 1:2.39.2-1.1 [2049 kB]
Get:4 https://deb.debian.org/debian bookworm/main amd64 git amd64 1:2.39.2-1.1 [7171 kB]
Get:5 https://deb.debian.org/debian bookworm/main amd64 patch amd64 2.7.6-7 [128 kB]
Fetched 9377 kB in 1s (16.8 MB/s)
Selecting previously unselected package liberror-perl.
(Reading database ... 68526 files and directories currently installed.)
Preparing to unpack .../liberror-perl_0.17029-2_all.deb ...
Unpacking liberror-perl (0.17029-2) ...
Selecting previously unselected package git-man.
Preparing to unpack .../git-man_1%3a2.39.2-1.1_all.deb ...
Unpacking git-man (1:2.39.2-1.1) ...
Selecting previously unselected package git.
Preparing to unpack .../git_1%3a2.39.2-1.1_amd64.deb ...
Unpacking git (1:2.39.2-1.1) ...
Selecting previously unselected package patch.
Preparing to unpack .../patch_2.7.6-7_amd64.deb ...
Unpacking patch (2.7.6-7) ...
Setting up liberror-perl (0.17029-2) ...
Setting up patch (2.7.6-7) ...
Setting up git-man (1:2.39.2-1.1) ...
Setting up git (1:2.39.2-1.1) ...
Processing triggers for man-db (2.11.2-2) ...
```

### Verify Git installation
```
$ git —version
git version 2.39.2
```


### Clone cbioportal-docker-compose repo:
```
$ git clone https://github.com/cBioPortal/cbioportal-docker-compose.git
Cloning into 'cbioportal-docker-compose'...
remote: Enumerating objects: 373, done.
remote: Counting objects: 100% (189/189), done.
remote: Compressing objects: 100% (116/116), done.
remote: Total 373 (delta 124), reused 95 (delta 68), pack-reused 184
Receiving objects: 100% (373/373), 84.60 KiB | 1.63 MiB/s, done.
Resolving deltas: 100% (188/188), done.
$ cd cbioportal-docker-compose
```

### Install Docker and verify installation:
```
$ sudo apt-get install docker.io
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu cgroupfs-mount containerd criu libbinutils libctf-nobfd0 libctf0 libgprofng0 libintl-perl libintl-xs-perl libjansson4
  libmodule-find-perl libmodule-scandeps-perl libnet1 libnftables1 libnl-3-200 libproc-processtable-perl libprotobuf32 libsort-naturally-perl libterm-readkey-perl needrestart
  python3-protobuf runc tini
Suggested packages:
  binutils-doc containernetworking-plugins docker-doc aufs-tools btrfs-progs debootstrap rinse rootlesskit xfsprogs zfs-fuse | zfsutils-linux needrestart-session
  | libnotify-bin iucode-tool
The following NEW packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu cgroupfs-mount containerd criu docker.io libbinutils libctf-nobfd0 libctf0 libgprofng0 libintl-perl libintl-xs-perl
  libjansson4 libmodule-find-perl libmodule-scandeps-perl libnet1 libnftables1 libnl-3-200 libproc-processtable-perl libprotobuf32 libsort-naturally-perl libterm-readkey-perl
  needrestart python3-protobuf runc tini
0 upgraded, 27 newly installed, 0 to remove and 2 not upgraded.
Need to get 74.8 MB of archives.
After this operation, 310 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 file:/etc/apt/mirrors/debian.list Mirrorlist [30 B]
Get:2 https://deb.debian.org/debian bookworm/main amd64 runc amd64 1.1.5+ds1-1+deb12u1 [2710 kB]
Get:3 https://deb.debian.org/debian bookworm/main amd64 containerd amd64 1.6.20~ds1-1+b1 [25.9 MB]
Get:4 https://deb.debian.org/debian bookworm/main amd64 tini amd64 0.19.0-1 [255 kB]
Get:5 https://deb.debian.org/debian bookworm/main amd64 docker.io amd64 20.10.24+dfsg1-1+b3 [36.2 MB]
Get:6 https://deb.debian.org/debian bookworm/main amd64 binutils-common amd64 2.40-2 [2487 kB]
Get:7 https://deb.debian.org/debian bookworm/main amd64 libbinutils amd64 2.40-2 [572 kB]
Get:8 https://deb.debian.org/debian bookworm/main amd64 libctf-nobfd0 amd64 2.40-2 [153 kB]
Get:9 https://deb.debian.org/debian bookworm/main amd64 libctf0 amd64 2.40-2 [89.8 kB]
Get:10 https://deb.debian.org/debian bookworm/main amd64 libgprofng0 amd64 2.40-2 [812 kB]
Get:11 https://deb.debian.org/debian bookworm/main amd64 libjansson4 amd64 2.14-2 [40.8 kB]
Get:12 https://deb.debian.org/debian bookworm/main amd64 binutils-x86-64-linux-gnu amd64 2.40-2 [2246 kB]
Get:13 https://deb.debian.org/debian bookworm/main amd64 binutils amd64 2.40-2 [65.0 kB]
Get:14 https://deb.debian.org/debian bookworm/main amd64 cgroupfs-mount all 1.4 [6276 B]
Get:15 https://deb.debian.org/debian bookworm/main amd64 libprotobuf32 amd64 3.21.12-3 [932 kB]
Get:16 https://deb.debian.org/debian bookworm/main amd64 python3-protobuf amd64 3.21.12-3 [245 kB]
Get:17 https://deb.debian.org/debian bookworm/main amd64 libnet1 amd64 1.1.6+dfsg-3.2 [60.3 kB]
Get:18 https://deb.debian.org/debian bookworm/main amd64 libnftables1 amd64 1.0.6-2+deb12u2 [299 kB]
Get:19 https://deb.debian.org/debian bookworm/main amd64 libnl-3-200 amd64 3.7.0-0.2+b1 [63.1 kB]
Get:20 https://deb.debian.org/debian bookworm/main amd64 criu amd64 3.17.1-2 [665 kB]
Get:21 https://deb.debian.org/debian bookworm/main amd64 libintl-perl all 1.33-1 [720 kB]
Get:22 https://deb.debian.org/debian bookworm/main amd64 libintl-xs-perl amd64 1.33-1 [15.6 kB]
Get:23 https://deb.debian.org/debian bookworm/main amd64 libmodule-find-perl all 0.16-2 [10.6 kB]
Get:24 https://deb.debian.org/debian bookworm/main amd64 libmodule-scandeps-perl all 1.31-2 [41.7 kB]
Get:25 https://deb.debian.org/debian bookworm/main amd64 libproc-processtable-perl amd64 0.634-1+b2 [43.1 kB]
Get:26 https://deb.debian.org/debian bookworm/main amd64 libsort-naturally-perl all 1.03-4 [13.1 kB]
Get:27 https://deb.debian.org/debian bookworm/main amd64 libterm-readkey-perl amd64 2.38-2+b1 [24.5 kB]
Get:28 https://deb.debian.org/debian bookworm/main amd64 needrestart all 3.6-4+deb12u1 [59.8 kB]
Fetched 74.8 MB in 2s (39.9 MB/s)       
Selecting previously unselected package runc.
(Reading database ... 69632 files and directories currently installed.)
Preparing to unpack .../00-runc_1.1.5+ds1-1+deb12u1_amd64.deb ...
Unpacking runc (1.1.5+ds1-1+deb12u1) ...
Selecting previously unselected package containerd.
Preparing to unpack .../01-containerd_1.6.20~ds1-1+b1_amd64.deb ...
Unpacking containerd (1.6.20~ds1-1+b1) ...
Selecting previously unselected package tini.
Preparing to unpack .../02-tini_0.19.0-1_amd64.deb ...
Unpacking tini (0.19.0-1) ...
Selecting previously unselected package docker.io.
Preparing to unpack .../03-docker.io_20.10.24+dfsg1-1+b3_amd64.deb ...
Unpacking docker.io (20.10.24+dfsg1-1+b3) ...
Selecting previously unselected package binutils-common:amd64.
Preparing to unpack .../04-binutils-common_2.40-2_amd64.deb ...
Unpacking binutils-common:amd64 (2.40-2) ...
Selecting previously unselected package libbinutils:amd64.
Preparing to unpack .../05-libbinutils_2.40-2_amd64.deb ...
Unpacking libbinutils:amd64 (2.40-2) ...
Selecting previously unselected package libctf-nobfd0:amd64.
Preparing to unpack .../06-libctf-nobfd0_2.40-2_amd64.deb ...
Unpacking libctf-nobfd0:amd64 (2.40-2) ...
Selecting previously unselected package libctf0:amd64.
Preparing to unpack .../07-libctf0_2.40-2_amd64.deb ...
Unpacking libctf0:amd64 (2.40-2) ...
Selecting previously unselected package libgprofng0:amd64.
Preparing to unpack .../08-libgprofng0_2.40-2_amd64.deb ...
Unpacking libgprofng0:amd64 (2.40-2) ...
Selecting previously unselected package libjansson4:amd64.
Preparing to unpack .../09-libjansson4_2.14-2_amd64.deb ...
Unpacking libjansson4:amd64 (2.14-2) ...
Selecting previously unselected package binutils-x86-64-linux-gnu.
Preparing to unpack .../10-binutils-x86-64-linux-gnu_2.40-2_amd64.deb ...
Unpacking binutils-x86-64-linux-gnu (2.40-2) ...
Selecting previously unselected package binutils.
Preparing to unpack .../11-binutils_2.40-2_amd64.deb ...
Unpacking binutils (2.40-2) ...
Selecting previously unselected package cgroupfs-mount.
Preparing to unpack .../12-cgroupfs-mount_1.4_all.deb ...
Unpacking cgroupfs-mount (1.4) ...
Selecting previously unselected package libprotobuf32:amd64.
Preparing to unpack .../13-libprotobuf32_3.21.12-3_amd64.deb ...
Unpacking libprotobuf32:amd64 (3.21.12-3) ...
Selecting previously unselected package python3-protobuf.
Preparing to unpack .../14-python3-protobuf_3.21.12-3_amd64.deb ...
Unpacking python3-protobuf (3.21.12-3) ...
Selecting previously unselected package libnet1:amd64.
Preparing to unpack .../15-libnet1_1.1.6+dfsg-3.2_amd64.deb ...
Unpacking libnet1:amd64 (1.1.6+dfsg-3.2) ...
Selecting previously unselected package libnftables1:amd64.
Preparing to unpack .../16-libnftables1_1.0.6-2+deb12u2_amd64.deb ...
Unpacking libnftables1:amd64 (1.0.6-2+deb12u2) ...
Selecting previously unselected package libnl-3-200:amd64.
Preparing to unpack .../17-libnl-3-200_3.7.0-0.2+b1_amd64.deb ...
Unpacking libnl-3-200:amd64 (3.7.0-0.2+b1) ...
Selecting previously unselected package criu.
Preparing to unpack .../18-criu_3.17.1-2_amd64.deb ...
Unpacking criu (3.17.1-2) ...
Selecting previously unselected package libintl-perl.
Preparing to unpack .../19-libintl-perl_1.33-1_all.deb ...
Unpacking libintl-perl (1.33-1) ...
Selecting previously unselected package libintl-xs-perl.
Preparing to unpack .../20-libintl-xs-perl_1.33-1_amd64.deb ...
Unpacking libintl-xs-perl (1.33-1) ...
Selecting previously unselected package libmodule-find-perl.
Preparing to unpack .../21-libmodule-find-perl_0.16-2_all.deb ...
Unpacking libmodule-find-perl (0.16-2) ...
Selecting previously unselected package libmodule-scandeps-perl.
Preparing to unpack .../22-libmodule-scandeps-perl_1.31-2_all.deb ...
Unpacking libmodule-scandeps-perl (1.31-2) ...
Selecting previously unselected package libproc-processtable-perl:amd64.
Preparing to unpack .../23-libproc-processtable-perl_0.634-1+b2_amd64.deb ...
Unpacking libproc-processtable-perl:amd64 (0.634-1+b2) ...
Selecting previously unselected package libsort-naturally-perl.
Preparing to unpack .../24-libsort-naturally-perl_1.03-4_all.deb ...
Unpacking libsort-naturally-perl (1.03-4) ...
Selecting previously unselected package libterm-readkey-perl.
Preparing to unpack .../25-libterm-readkey-perl_2.38-2+b1_amd64.deb ...
Unpacking libterm-readkey-perl (2.38-2+b1) ...
Selecting previously unselected package needrestart.
Preparing to unpack .../26-needrestart_3.6-4+deb12u1_all.deb ...
Unpacking needrestart (3.6-4+deb12u1) ...
Setting up binutils-common:amd64 (2.40-2) ...
Setting up libctf-nobfd0:amd64 (2.40-2) ...
Setting up libnet1:amd64 (1.1.6+dfsg-3.2) ...
Setting up runc (1.1.5+ds1-1+deb12u1) ...
Setting up libjansson4:amd64 (2.14-2) ...
Setting up libmodule-find-perl (0.16-2) ...
Setting up tini (0.19.0-1) ...
Setting up libprotobuf32:amd64 (3.21.12-3) ...
Setting up libproc-processtable-perl:amd64 (0.634-1+b2) ...
Setting up libnl-3-200:amd64 (3.7.0-0.2+b1) ...
Setting up libintl-perl (1.33-1) ...
Setting up cgroupfs-mount (1.4) ...
Setting up libterm-readkey-perl (2.38-2+b1) ...
Setting up libbinutils:amd64 (2.40-2) ...
Setting up python3-protobuf (3.21.12-3) ...
Setting up containerd (1.6.20~ds1-1+b1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/containerd.service → /lib/systemd/system/containerd.service.
Setting up libsort-naturally-perl (1.03-4) ...
Setting up libmodule-scandeps-perl (1.31-2) ...
Setting up libctf0:amd64 (2.40-2) ...
Setting up libnftables1:amd64 (1.0.6-2+deb12u2) ...
Setting up docker.io (20.10.24+dfsg1-1+b3) ...
Adding group `docker' (GID 111) ...
Done.
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /lib/systemd/system/docker.service.
Created symlink /etc/systemd/system/sockets.target.wants/docker.socket → /lib/systemd/system/docker.socket.
Setting up libintl-xs-perl (1.33-1) ...
Setting up libgprofng0:amd64 (2.40-2) ...
Setting up criu (3.17.1-2) ...
Setting up binutils-x86-64-linux-gnu (2.40-2) ...
Setting up binutils (2.40-2) ...
Setting up needrestart (3.6-4+deb12u1) ...
Processing triggers for man-db (2.11.2-2) ...
Processing triggers for libc-bin (2.36-9+deb12u7) ...

$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c1ec31eb5944: Pull complete 
Digest: sha256:94323f3e5e09a8b9515d74337010375a456c909543e1ff1538f5116d38ab3989
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```


### Install Docker Compose as a plugin:
```
$ mkdir -p ~/.docker/cli-plugins
$ sudo curl -SL "https://github.com/docker/compose/releases/download/v2.18.1/docker-compose-linux-$(uname -m)" -o ~/.docker/cli-plugins/docker-compose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
100 52.0M  100 52.0M    0     0   102M      0 --:--:-- --:--:-- --:--:--  102M
$ sudo chmod +x ~/.docker/cli-plugins/docker-compose
$ docker compose version
Docker Compose version v2.18.1
```

If you get a permissions error when trying to install or use Docker Compose, try
```
$ sudo usermod -aG docker $USER
		replace $USER with your name:
$ groups $USER
		should see “docker” included in groups list
$ newgrp docker
```
Replace $USER with your username. You should now see "docker" included in the groups list.

### Install necessary data and config files:
```
$ ./init.sh
Unable to find image 'cbioportal/cbioportal:6.0.5' locally
6.0.5: Pulling from cbioportal/cbioportal
23828d760c7b: Pulling fs layer
dfc0d9a6855e: Pulling fs layer
3026e8edc115: Pulling fs layer
cd470b4ec28d: Pulling fs layer
6789efe2b2c4: Pulling fs layer
744c3a1efbf6: Pulling fs layer
570892e47ae9: Pulling fs layer
3628a4184ed4: Pulling fs layer
d2f72d5bf3a3: Pulling fs layer
55837616768a: Pulling fs layer
325f5a28c44e: Pulling fs layer
9d6fe83c55de: Pulling fs layer
2ed8a9bd24be: Pulling fs layer
97fc675ebd13: Pulling fs layer
e0a9c35d6dbb: Pulling fs layer
a08bb2d7fa7e: Pulling fs layer
cd470b4ec28d: Waiting
6789efe2b2c4: Waiting
744c3a1efbf6: Waiting
570892e47ae9: Waiting
3628a4184ed4: Waiting
d2f72d5bf3a3: Waiting
55837616768a: Waiting
325f5a28c44e: Waiting
9d6fe83c55de: Waiting
2ed8a9bd24be: Waiting
97fc675ebd13: Waiting
e0a9c35d6dbb: Waiting
a08bb2d7fa7e: Waiting
23828d760c7b: Verifying Checksum
23828d760c7b: Download complete
dfc0d9a6855e: Verifying Checksum
dfc0d9a6855e: Download complete
cd470b4ec28d: Verifying Checksum
cd470b4ec28d: Download complete
6789efe2b2c4: Verifying Checksum
6789efe2b2c4: Download complete
570892e47ae9: Verifying Checksum
570892e47ae9: Download complete
3026e8edc115: Verifying Checksum
3026e8edc115: Download complete
d2f72d5bf3a3: Verifying Checksum
d2f72d5bf3a3: Download complete
744c3a1efbf6: Verifying Checksum
744c3a1efbf6: Download complete
55837616768a: Verifying Checksum
55837616768a: Download complete
325f5a28c44e: Verifying Checksum
325f5a28c44e: Download complete
9d6fe83c55de: Verifying Checksum
9d6fe83c55de: Download complete
97fc675ebd13: Verifying Checksum
97fc675ebd13: Download complete
23828d760c7b: Pull complete
e0a9c35d6dbb: Verifying Checksum
e0a9c35d6dbb: Download complete
a08bb2d7fa7e: Verifying Checksum
a08bb2d7fa7e: Download complete
2ed8a9bd24be: Verifying Checksum
2ed8a9bd24be: Download complete
dfc0d9a6855e: Pull complete
3628a4184ed4: Verifying Checksum
3628a4184ed4: Download complete
3026e8edc115: Pull complete
cd470b4ec28d: Pull complete
6789efe2b2c4: Pull complete
744c3a1efbf6: Pull complete
570892e47ae9: Pull complete
3628a4184ed4: Pull complete
d2f72d5bf3a3: Pull complete
55837616768a: Pull complete
325f5a28c44e: Pull complete
9d6fe83c55de: Pull complete
2ed8a9bd24be: Pull complete
97fc675ebd13: Pull complete
e0a9c35d6dbb: Pull complete
a08bb2d7fa7e: Pull complete
Digest: sha256:56ed20235fabcd601a76a9dfabc92e0b91bc1f5d8f14200b98c5f79846eef51b
Status: Downloaded newer image for cbioportal/cbioportal:6.0.5
--2024-06-25 15:29:42--  https://github.com/cBioPortal/datahub/raw/master/seedDB/seedDB_hg19_archive/seed-cbioportal_hg19_v2.12.14.sql.gz
Resolving github.com (github.com)... 140.82.112.4
Connecting to github.com (github.com)|140.82.112.4|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://raw.githubusercontent.com/cBioPortal/datahub/master/seedDB/seedDB_hg19_archive/seed-cbioportal_hg19_v2.12.14.sql.gz [following]
--2024-06-25 15:29:42--  https://raw.githubusercontent.com/cBioPortal/datahub/master/seedDB/seedDB_hg19_archive/seed-cbioportal_hg19_v2.12.14.sql.gz
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.110.133, 185.199.109.133, 185.199.108.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.110.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 51337072 (49M) [application/octet-stream]
Saving to: ‘seed.sql.gz’

seed.sql.gz                                  100%[============================================================================================>]  48.96M   185MB/s    in 0.3s    

2024-06-25 15:29:43 (185 MB/s) - ‘seed.sql.gz’ saved [51337072/51337072]

--2024-06-25 15:29:43--  https://cbioportal-datahub.s3.amazonaws.com/lgg_ucsf_2014.tar.gz
Resolving cbioportal-datahub.s3.amazonaws.com (cbioportal-datahub.s3.amazonaws.com)... 52.216.177.203, 52.216.205.123, 52.216.43.185, ...
Connecting to cbioportal-datahub.s3.amazonaws.com (cbioportal-datahub.s3.amazonaws.com)|52.216.177.203|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 739531 (722K) [application/x-tar]
Saving to: ‘lgg_ucsf_2014.tar.gz’

lgg_ucsf_2014.tar.gz                         100%[============================================================================================>] 722.20K  --.-KB/s    in 0.1s    

2024-06-25 15:29:43 (4.95 MB/s) - ‘lgg_ucsf_2014.tar.gz’ saved [739531/739531]

lgg_ucsf_2014/
lgg_ucsf_2014/LICENSE
lgg_ucsf_2014/case_lists/
lgg_ucsf_2014/case_lists/cases_sequenced.txt
lgg_ucsf_2014/case_lists/cases_all.txt
lgg_ucsf_2014/data_mutations.txt
lgg_ucsf_2014/data_timeline_treatment.txt
lgg_ucsf_2014/meta_mutations.txt
lgg_ucsf_2014/meta_clinical_sample.txt
lgg_ucsf_2014/meta_timeline_status.txt
lgg_ucsf_2014/data_clinical_patient.txt
lgg_ucsf_2014/meta_study.txt
lgg_ucsf_2014/data_timeline_surgery.txt
lgg_ucsf_2014/meta_clinical_patient.txt
lgg_ucsf_2014/meta_timeline_treatment.txt
lgg_ucsf_2014/data_timeline_status.txt
lgg_ucsf_2014/data_clinical_sample.txt
lgg_ucsf_2014/meta_timeline_surgery.txt
lgg_ucsf_2014/meta_timeline_specimen.txt
lgg_ucsf_2014/data_timeline_specimen.txt
```

### "Prime" the database container
```
$ docker compose up cbioportal-database
```
Kill the container (Ctrl-C) once it runs.

### Configure ports
```
$ docker run -d --name cbioportal-container -v /home/usr/cbioportal-docker-compose/data/cgds.sql:/docker-entrypoint-initdb.d/cgds.sql \
-v /home/usr/cbioportal-docker-compose/data/seed.sql.gz:/docker-entrypoint-initdb.d/seed.sql.gz \
-v /home/usr/cbioportal-docker-compose/images/cctg_logo.png:/cbioportal-webapp/images/cctg_logo.png \
-p 8080:8080 -p 27017:27017 -p 8000:8000 -p 8001:8001 -p 8081:8081 -p 8082:8082 -p 8083:8083 -p 8084:8084 cbioportal/cbioportal
```

### Compose all containers
You now have the cbioportal-container running, but we want all four containers to run simultaneously. Now that the ports are configured,
you need to stop the previous image from running.
```
$ docker stop $(docker ps -aq)
$ docker compose up
```
Verify that containers are accessible at

  http://$EXTERNAL_IP:8080
	
Replace $EXTERNAL_IP with your VM’s external IP.

If you encounter **Error response from daemon: Conflict. The container name "/cbioportal-container" is already in use by container 
"bd5ea9bef51f44d340da6e8e5bc0775cc9580f53352d884b3d9ce2e5ff58fe10". You have to remove (or rename) that container to be able to reuse that name.**

First try simply removing the container and rerunning docker compose up
```
$ docker rm -f cbioportal-container
$ docker compose up
```
If that doesn't fix the issue, kill the containers (Ctrl-c), and run
```
$ docker compose down -v
$ docker compose up
```


