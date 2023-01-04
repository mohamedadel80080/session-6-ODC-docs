
## docker compose

### The advantage
It helps you create your tasks faster and write fewer commands



step 1 
create ` docker-compose.yml `

step 2 


```bash
version: "3" #composer version
services:
  node-app:
    container_name: express-node-app-container #contaniner name
    ports:
      - "4000:4000" #ports
    build: .  #to connect Dockerfile
    volumes:
      -./scr:/app/scr:ro #hot relod
```
run ` docker-cmposer up -d ` to build container


## Docker Docs 

Part 1 : Docker Hot Reload

` npm i nodemon `

```
FROM node:18

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 4000

CMD [ "npm", 'start' ]
```
and

` docker run --name express-node-app-container -d -p 4000:4000 express-node-app " . ` to run container

#### Case 1 
When doing this, it causes us a problem. If something is deleted from inside the container, it is deleted from the main files
#### FIX
` docker run --name express-node-app-container -v pathfile:app:ro -d -p 4000:4000 express-node-app " . ` to run container

#### Case  2 
If something is deleted from the outside by mistake, it is not deleted from the inside of the container

#### FIX
` docker run --name express-node-app-container -v pathfile:app:ro -v /app/file -d -p 4000:4000 express-node-app " . ` to run container


### Case 3 (environment)
Sometimes we face problems in uploading the application to more than one work environment, such as development, testing, and production


#### FIX

Create Docker file (Stage)
Example ` docker-compose-dev.yml ` and Create environment code

```
version: "3" #composer version
services:
  node-app:
    container_name: express-node-app-container-dev #contaniner name
    build: .
    ports:
      - "4000:4000" #ports
      #to connect Dockerfile
    environment:
      - NODE_ENV=development
 ```
      
       
## Running Tests

To run tests, run the following command

```bash
  npm run test
```


## commend

` docker build -t "express-node-app" . ` to run image 

` docker run --name express-node-app-container -d -p 4000:4000 express-node-app " . ` to run container

` docker exec -it express-node-app-container bash   ` to run commend from container

` docker logs  express-node-app-container   ` to view logs from container

` docker rm  express-node-app-container -f ` to remove container

` docker-cmposer up -d ` to build container

` docker -help ` to build container



