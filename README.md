# Setup Steps for running Locally

## Prerequisites:
- dev tools installed( vs code, git, node 10.16.0, npm, docker)

### O4S config
copy the following file to your local machine 
```
 "IP": "localhost",
    "PORT": 27017,
    "STRATEGY": "none"
  },
  "UID_MANAGER": {
    "IP": "localhost",
    "PORT": 8080,
    "PROTOCOL": "http"
  },
  "WMS_BACKEND": {
    "IP": "127.0.0.1",
    "PORT": 9090
  },
  "LABEL_PRINTER_BACKEND": {
    "IP": "localhost",
    "PORT": 7000,
    "PROTOCOL": "http"
  },
  "LABEL_PRINTER_CLIENT": {
    "PROTOCOL": "http",
    "IP": "localhost",
    "PORT": 6060
  },
  "SERIALIZER_BACKEND": {
    "PROTOCOL": "http",
    "IP": "127.0.0.1",
    "PORT": 51988
  },
  "MARK_CONSOLE_CLIENT": {
    "PROTOCOL": "http",
    "IP": "192.168.225.31",
    "PORT": 6060
  },
  "AUTH_SERVICE_HOST": "https://stag.o4s.io/auth",
  "INVENTORY_SERVICE_HOST": "https://stag.o4s.io",
  "auth": {
    "client_id": "o4s.auth-broker",
    "client_secret": "9f234c44-b976-4749-aa9a-aef35a689ba5"
  },
  "PRE_PRINTED_UID_SYNC_BATCH_SIZE": 200,
  "AUTO_REMOVE_SYNCED_UIDS": {
    "shouldRemove": true,
    "runningInterval": {
      "value": 4,
      "unit": "DAYS"
    }
  },
  "CSN_JOB_ALLOWED": true
}
```
and add this path in ``.bashrc``

```
export O4S_CONFIG_PATH="/home/charan/code-directory/config.json"

```
and run 

```
$ source ~/.bashrc

```

### node configs
```
$ npm config set registry "http://registry.npmjs.org/"

# 10.16.0 seems to be the popular version among us

$ nvm install 10.16.0
$ nvm use 10.16.0
$ nvm alias default 10.16.0

```
add this line to .bashrc
```
$ export NODE_ENV="dev"

```
and run 

```
$ source ~/.bashrc

```
### mongodb setup

run mongo locally through docker:

````
$ docker pull mongo  #get image

$ docker run --network=host --name localhost-mongo -d mongo:latest  # run docker container on localhost network and copy container ID

$ docker ps # verify the container is running 

$ docker exec -it <container ID> /bin/bash # log into to the container shell

$ mongo # open mongo shell


````


connect to the db via gui (compass) with the uri below

```
mongodb://localhost:27017
```
### Clone the git repo 
```
$ git clone -b 'master-mark' git@github.com:original4sure/clients.git
```

### Run the packages in the clients repo

create a ``.env`` file inside ``mark-console-ui``
```
VUE_APP_IS_DUMMY=false
VUE_APP_API_URL=http://localhost:51988

```

build and run modules using 
```
npm i
npm run dev (or) npm run serve

```
