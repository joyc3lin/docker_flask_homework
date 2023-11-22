# docker_flask_homework
This assignment aims to provide hands-on experience in Dockerizing Flask applications, first individually and then using Docker Compose for managing multiple applications.

# Part One: Dockerizing a Single Flask Application

+ In the <code>Part1</code> folder, Create a flask application 
+ Write a Dockerfile to containerize this Flask application
+ Enter the following into the Dockerfile: 

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

+ Build a docker image named [iamge-name] with : <code>docker -t [image-name] . </code>
    + Dont forget the decimal at the end, it's needed to take all files in directory 
+ To see list of existing images, run: <code>docker images</code>
+ Run the image with: <code>docker run -p [machine-port-number]:[docker-image-port-number] [image-name]</code>
    + make sure the port being used to run the application matches the port number for [machine-port-number]
+ To see a list of running containers: <code>docker ps</code>

# Part Two: Multi-Container Setup with Docker Compose

+ In the <code>Part2</code> folder, create two distinct Flask applications in <code>Flask1</code> and <code>Flask2</code>
    + Follow the steps from Part One on how to build a flask application with Docker 
+ Create a <code>docker-complose.yml</code> file and fill it with: 

```python
# docker compose version 
version: '3'

# list of different containers in the application
services:

# first flask app
  flask_app_1:
    # directs the image being built to Flask1's dockerfile
    build: ./Flask1
    # uses port 5001 for host and 5000 for container 
    ports:
      - "5001:5000"
    # changes in local files will be brought to the application 
    volumes:
      - ./Flask1:/app
```
+ Dockerizing with Docker Compose: <code>docker-compose up --build <code>
    + Wait for applicatiosn to be built, this might take a while
+ The applications can be rerun with <code>docker-compose up</code>

# Challenges and Comments 

+ Dockerizing with Docker Compose vs with Docker alone: 
    + Docker Compose allows users to dockerize multiple services/applications with one file while docker alone only allows for one 
      
+ Challenge:
    + _Running <code>docker-compose up --build</code>_: Ran into an error running this line. Issue was in the <code>docker-complose.yml</code> file. Under Build and Volumes, the name of the file directory was lowercase while the folder's name had the first letter capitalized. The code ran noramally once they were made the same.  
