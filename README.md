# nodebb-docker-dev

A docker chain of Nginx, NodeBB, Redis based on [Alpine Linux](http://www.alpinelinux.org) for mainly developments and small standalone service. 

## Introduction

## TL;DR
You will get error of a nginx docker if you already have any web server with 80 port.
```
git clone https://github.com/qgp9/nodebb-docker-dev.git nodebb-docker-dev
cd nodebb-docker-dev
git clone -b v1.x.x https://github.com/NodeBB/NodeBB.git nodebb
./bin/com-nodebb npm install
./bin/docker-compose up -d 
./bin/com-nodebb ./nodebb setup  
  # URL used to access this NodeBB  => ex) http://example.com ( DON'T ADD 4567 )
  # Which database to use (mongo)   => redis
  # Just use default vaules for other ( means just enter ), except Administartor user information ( use your own ).
./bin/docker-compose up -d 
```
* Now visit your url with a web brower
  * A type of Database : redis
  * Host IP or address of your Redis instance : redis
  * ![configuration screen shot](http://i.imgur.com/Pd2TLTH.png)

# Command line Settings, Upgrade, npm  and so on
```
./bin/com-nodebb ./nodebb setup
./bin/com-nodebb ./nodebb upgrade
./bin/com-nodebb npm install <package>
```
* You **DONOT** `npm <install|update|whatever>` on a host directory( `nodebb-docker-dev/nodebb` ) out of a docker container.
* But editings is fine

## Details will be .. later
