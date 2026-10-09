# Exercise 4: Docker Networking

## Objective

To understand Docker bridge networking and enable communication between multiple containers using container names.

## Technologies Used

* Docker
* Python
* Flask
* MySQL
* Redis

## Project Files

* `app.py` - Flask REST API
* `Dockerfile` - Instructions to build the Flask image
* `requirements.txt` - Python dependencies

## Docker Network

Created a custom bridge network named `my-bridge-net`.

```powershell
docker network create --driver bridge my-bridge-net
```

## Build the Flask Image

```powershell
docker build -t flask-api .
```

## Run the Containers

```powershell
docker run -d --name mysql --network my-bridge-net -e MYSQL_ROOT_PASSWORD=labpassword mysql:latest

docker run -d --name redis --network my-bridge-net redis:latest

docker run -d --name flask --network my-bridge-net -p 5001:5001 flask-api
```

## Test the Flask API

Open http://localhost:5001/about in a browser.

## Verify Container Networking

```powershell
docker ps
docker network inspect my-bridge-net
docker exec -it flask bash
```

Inside the Flask container:

```bash
getent hosts mysql
getent hosts redis
ping -c 4 mysql
ping -c 4 redis
```

## Result

The Flask, MySQL, and Redis containers were started on the custom Docker bridge network. API and networking test results should be recorded after verification.
