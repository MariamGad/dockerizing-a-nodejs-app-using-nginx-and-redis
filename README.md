# dockerizing-a-nodejs-app-using-nginx-and-redis
## Overview
We want to containerize a three tier application that consists of
* **NGINX**: exposed to the internet and works as a load balancer. 
* **Web1** , **Web2**: both are Node.js application, expose a specific port (this port is used by NGINX to communicate with the app).
* **RedisDB**: the application is going to do some processing which is will be stored in this database.
