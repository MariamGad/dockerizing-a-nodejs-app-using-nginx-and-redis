# dockerizing-a-nodejs-app-using-nginx-and-redis
## Overview
We want to containerize a three tier application that consists of
* **NGINX:** exposed to the internet and works as a load balancer. 
* **Web1** , **Web2:** both are Node.js application, expose a specific port (this port is used by NGINX to communicate with the app).
* **RedisDB:** the application is going to count the number of the visits and store it in this database.

## Steps
### NGINX
* add your load balancing configuration in `nginx.conf` file 
* create Dockerfile from `nginx image` then add the configuration file `nginx.conf` under `/etc/nginx/conf.d`


### Web1 , Web2
these steps are done for both servers 
* create a nodejs file `server.js` to update the number of visits of the web application in redisDB.
* create `package.json` file to add all the information about the app and the dependencies that be installed. 
* Create Dockerfile from `node:alpine image`, copy all these files under `/usr/src/app`, install nodejs package manager `npm` and finally when the container launch run `server.js`.

### docker-compose file
we will add four services in that file 
#### 1. NGINX
* NGINX service will be built from the created `Dockerfile` that is mentioned above.
* this service will depend on our both `web servers`.
* and will listen on port `80` which is going to be mapped to port `80` on host.

#### 2. Redis
* Redis database service will be built from `redis:alpine`.
* and will listen on port `6379` which is going to be mapped to port `6379` on host.

#### 3. Web1, Web2
* both services will be built from a different `Docker file` as mentioned above.
* both will depend on the `redis database`
* both web1 and “web2” services listen on port `5000` and will be mapped to ports `81` and `82` on host.
