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
