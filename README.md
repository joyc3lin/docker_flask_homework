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

# Part Two: Multi-Container Setup with Docker Compose

+ create two distinct Flask applications
+ 