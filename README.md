 readme of docker deployment


 A simple node.js + MongoDB + Mongo express app 

 Node.js is used for backend 
 Mongo DB is used ofr database 
 Mongo express for UI 
 Works locally 


  (https://gitlab.com/nanuchi/techworld-js-docker-demo-app)

---

````markdown
# Node.js Docker Local Deployment

This project is a simple Node.js + Express app connected to a MongoDB database and managed through Mongo Express.  
It’s based on [TechWorld with Nana’s demo](https://gitlab.com/nanuchi/techworld-js-docker-demo-app), which I customized to run locally using Docker containers.

---

## What I Did

- Cloned the original TechWorld with Nana repository  
- Navigated into the **app** folder:
  ```bash
  cd app
````

* Installed dependencies using:

  ```bash
  npm install
  ```
* Started the app locally with:

  ```bash
  node server.js
  ```
* Pulled the official Docker images for MongoDB and Mongo Express:

  ```bash
  docker pull mongo
  docker pull mongo-express
  ```
* Created a custom Docker network for both containers:

  ```bash
  docker network create mongo-net
  ```
* Ran a MongoDB container with the required environment variables:

  ```bash
  docker run -d \
    --name mongodb \
    --network mongo-net \
    -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=admin \
    -e MONGO_INITDB_ROOT_PASSWORD=password \
    mongo
  ```
* Ran a Mongo Express container connected to the same network:

  ```bash
  docker run -d \
    --name mongoexpress \
    --network mongo-net \
    -p 8081:8081 \
    -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
    -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
    -e ME_CONFIG_MONGODB_SERVER=mongodb \
    mongo-express
  ```
* Opened **Mongo Express UI** at [http://localhost:8081](http://localhost:8081)
  and created a new database called `my-db` with a collection named `users`.
* Connected the Node.js app to MongoDB using the connection string in `server.js`.

---

## Run Locally

Make sure your MongoDB container is running before starting the app.

```bash
node app/server.js
```

Then visit:
[http://localhost:3000](http://localhost:3000)

Mongo Express is available at:
[http://localhost:8081](http://localhost:8081)

---

## Project Stack* Node.js – Express backend
* MongoDB – Database
* Mongo Express – Web UI for MongoDB
* Docker – Container management

---

## Notes


---

## Author

**Shubham (@Shubh1699)**
Customized and containerized version of TechWorld with Nana’s Node.js Docker demo.

```

---


~

