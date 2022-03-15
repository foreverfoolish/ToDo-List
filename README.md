ToDo App

Hello! This is a simple ToDo webapp built using React, Django and MongoDB. PLEASE READ THE UPDATED SETUP INSTRUCTIONS CAREFULLY TO GET THE PROJECT RUNNING.

There were many mistakes in the initial docker-compose.yml and Dockerfile files that I have debugged and sorted out. Use of obsolete installation methods (eg. easy_install) was made that I replaced with updated and contemporary methods. 

I then worked on the API (views.py file) and created a working API that handles Get and Post requests. 

Creating the frontend using React useState hooks and props was a simple task.

*To test the API, go to http://localhost:8000/todos and insert values in key:value pair format with key = "name", for example:

```
{"name":"todo_item"}
```

Replace todo_item with whatever you'd like to add.


# Structure

This repository includes code for a Docker setup with 3 containers:
* App: This is the React dev server and runs on http://localhost:3000. The code for this resides in src/app directory.
* API: This is the backend container that run a Django instance on http://localhost:8000. 
* Mongo: This is a DB instance running on port 27017. Django views already have code written to connect to this instance of Mongo.

# Setup
1. Clone this repository
```
git clone https://github.com/foreverfoolish/adb_sol_2
```
2. Change into the cloned directory and set the environment variable for the code path. Replace `path_to_repository` appropriately.
```
export ADBREW_CODEBASE_PATH= 'path_to_repository'
```
3. Build container (you only need to build containers for the first time or if you change image definition, i.e., `Dockerfile`). This step will take a good amount of time.
```
docker-compose build
```
* Use -E flag if it can't get the code path right.
```
sudo -E docker-compose build
```
4. Once the build is completed, start the containers:
```
docker-compose up -d
```
*Again, use -E flag like in step 3 if docker-compose gives any trouble.
5. Once complete, `docker ps` should output something like this:
```
CONTAINER ID   IMAGE               COMMAND                  CREATED         STATUS         PORTS                      NAMES
e445be7efa61   adbrew_test_api     "bash -c 'cd /src/re…"   3 minutes ago   Up 2 seconds   0.0.0.0:8000->8000/tcp     api
0fd203f12d8a   adbrew_test_app     "bash -c 'cd /src/ap…"   4 minutes ago   Up 3 minutes   0.0.0.0:3000->3000/tcp     app
884cb9296791   adbrew_test_mongo   "/usr/bin/mongod --b…"   4 minutes ago   Up 3 minutes   0.0.0.0:27017->27017/tcp   mongo
```
6. Check that you are able to access http://localhost:3000 and http://localhost:8000/todos

# Tips
1. Once containers are up and running, you can view container logs by executing `docker logs -f --tail=100 {container_name}` Replace `container_name` with `app` or `api`(output of `docker ps`)
2. You can enter the container and inspect it by executing `docker exec -it {container_name} bash` Replace `{container_name}` with `app` or `api` (output of `docker ps`)
3. Shut all containers using `docker-compose down`
4. Restart a container using `docker restart {container_name}`
