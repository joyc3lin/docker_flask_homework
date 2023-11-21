# docker_flask_homework
This assignment aims to provide hands-on experience in Dockerizing Flask applications, first individually and then using Docker Compose for managing multiple applications.

# Part One: Dockerizing a Single Flask Application

+ Create flask application: requirements.tct file
+ Write a Dockerfile to containerize this Flask application

```python
# pull a specific version of python from the docker hub
FROM python:3.10-slim-buster
# creating new virtual OS 
WORKDIR /app
# puts files in directory and places it in virtual OS
COPY . /app/
# installs requprements.txt file
RUN pip install -r requirements.txt
# exposes port 5000 to virtual OS to enable communication
EXPOSE 5000
# run command to run web application
CMD ["python", "app.py"]
```

+ Build the Docker image and run the container
    + start by building a docker image named [iamge-name] : <code>docker -t [image-name] . </code>
    + Dont forget the decimal at the end, needed to take all files in directory 
+ To see list of existing images, run: <code>docker images</code>
+ run image with: <code>docker run -p [machine-port-number]:[docker-image-port-number] [image-name]</code>
    + make sure the port being used matches the port number for [machine-port-number]
+ To see a list of running containers: <code>docker ps</code>
+ Type docker stop <container ID>. This will stop your container.
+ Type docker rm <container ID>. This will remove your container.

# Part Two: Multi-Container Setup with Docker Compose

+ create two distinct Flask applications
+ create a docker-complose.yml file 

```python
# docker compose version 
version: '3'

# list of different containers in the application
services:

# first flask app
  flask_app_1:
    # directs the image being built to Flask1's dockerfile
    build: ./flask1
    # uses port 5001 for host and 5000 for container 
    ports:
      - "5001:5000"
    # changes in local files will be brought to the application 
    volumes:
      - ./flask1:/app
```
+ build 2 flask files 
+ Dockerizing with Docker Compose
+ docker-compose up --build 
+ if you ctrl+c out, you can rerun the flask apps with docker-compose up 

# Challenges and Comments 

+ Dockerizing with Docker Compose
+ challenges encountered