Script for fuzzing ffmpeg's opus decoder with American Fuzzy Lop.

https://twitter.com/obencoder/status/639841151802019841

# How to use

## 1. install docker(choice 1)

    sudo apt-get install docker.io
    curl -s https://get.docker.io/ubuntu/ | sudo sh
    
    docker -v
    
## 2. docker settings

    sudo ufw allow 4243/tcp
    sudo groupadd docker
    sudo gpasswd -a ${USER} docker
    sudo service docker restart

## 3. install docker image & run

    git clone https://github.com/Oss9935/afl-ffmpeg-opus.git
    cd afl-ffmpeg-opus
    sudo docker build -t bbkim/afl-ffmpeg-opus .
    sudo docker run -u 0 -i -t --ulimit core=-1 --privileged bbkim/afl-ffmpeg-opus /bin/bash

## 4. do fuzz with afl

    sudo echo core >/proc/sys/kernel/core_pattern ./afl-1.92b/afl-fuzz -i ./opus_testvectors/ -o ./findings/ ./ffmpeg/ffmpeg
