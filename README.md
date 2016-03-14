# nodebb-docker-dev

[![Join the chat at https://gitter.im/qgp9/nodebb-docker-dev](https://badges.gitter.im/qgp9/nodebb-docker-dev.svg)](https://gitter.im/qgp9/nodebb-docker-dev?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

A docker chain of Nginx, NodeBB, MongoDB, Redis based on [Alpine Linux](http://www.alpinelinux.org) for mainly developments and small standalone service. 

## **!!! WARNING !!!**
I haven't checked yet how `mongod` and `redis-server` manage `SIGTERM` which docker send.
This means that in worst case one can loose data !
Does any body know about this?

## TL;DR
You will get error of a nginx docker if you already have any web server with 80 port.
```
git clone https://github.com/qgp9/nodebb-docker-dev.git nodebb-docker-dev
cd nodebb-docker-dev
git clone -b v1.x.x https://github.com/NodeBB/NodeBB.git nodebb
./bin/com-nodebb npm install
./bin/com-nodebb npm install socket.io-redis connect
./bin/com-nodebb npm setup
./bin/utils jq -M -s add nodebb/config.json conf/example/redis.josn > tmp.json && mv tmp.json nodebb/config.json
./bin/docker-compose up 
```
* DB: `mongo` , DB address: `mongodb` , DB user: `admin` , no DB password

# Command line Settings, Upgrade, npm  and so on
```
./bin/com-nodebb ./nodebb setup
./bin/com-nodebb ./nodebb upgrade
./bin/com-nodebb npm install <package>
```
* You **DONOT** `npm <install|update|whatever>` on a host directory( `nodebb-docker-dev/nodebb` ) out of a docker container.
* But editings are fine

## Structure
```
nodebb-docker-dev
├── bin   
│   ├── com-nodebb      # Helper to control NodeBB docker
│   └── docker-compose  # Docker version of docker-compose for portable
├── conf                # All Dockerfile and configuration.
│   ├── nginx
│   │   ├── Dockerfile
│   │   └── nginx.conf
│   ├── nodebb-dev
│   │   └── Dockerfile
│   └── redis
│       ├── Dockerfile
│       └── redis.conf
├── data
│   ├── nginx
│   │   └── logs         # nginx, site logs
│   ├── nodebb           # Empty. reserved for future plans.
│   └── redis            # dump.rgb ( db data ) , redis.log ( log file ) 
├── docker-compose.yml
└── nodebb               # NodeBB source will be here 
```
* All configuration, data( log file ), NodeBB codes are mounted to dockers ( not copied ). So you can just edit them on a host directory.
* All configurations are in a `conf` directory. All data files genereated by nginx, redis are in a `data` directory.
  * Exceptionally `config.json` and a logfile of NodeBB are in nodebb directory for easy management.
* This desigin is aimed to archive best development/management of small standalone service. 
  * Every improtant files are just under a main directory on a host and dockers are just like applications, 
  * so you can remove/rebuild docker containers/images freely without any effect to data.
  * Also you can easily migrate this chain to new server. What you need is just copy the main directory to new server and rebuild dockers.
  * But large distributing/scaling can meet some side effects. 

## Project Name
When you build a system by `./bin/docker-compose up`, you will see a wired long name of images/container like `nodebbdockerdev_nginx` by `docker images` or `docker ps -a`. This is because `docker-compose` use a directory name as a project nam.
To get a short/readable name , you have recommontable 2 options.
  1. Change the directory name
  2. Shell variables ( **RECOMMENDED** but easilly one can make mistakes. [smartcd](https://github.com/cxreg/smartcd) can help )
     * `export COMPOSE_PROJECT_NAME=qgp9`
     * or you can embed this variable to `./bin/com-nodebb` and `./bin/docker-compose`
Then you will see `qgp9_nginx`.

## Details will be .. later
