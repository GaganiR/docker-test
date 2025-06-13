# Using Docker To Containerize Python App
This project shows how to containerize a simple Python script (app.py) using Docker, and run it from an Amazon EC2 instance, and push the built Docker image to Docker Hub. 
## Prerequisites
Launch an EC2 Instance.
Connect via SSH:
```
ssh -i <your-key.pem> ec2-user@<ec2-public-ip>
```
## INSTALL DOCKER
```
sudo apt update
sudo apt install docker.io -y
```
## Start Docker daemon
 Verify if the docker daemon is actually started and Active
 ```
sudo systemctl status docker
```
![check docker running](https://github.com/user-attachments/assets/8d196e16-0c40-48ec-ae94-6267b1a9ba21)

If its, not started, use the below command 
```
sudo systemctl start docker
```
Always ensure the docker daemon is up and running.
## Start Docker and Grant Access
An easy way to verify your Docker installation is by running the below command
```
docker run hello-world
```
If the output says: Permission denied
It means that your user does not have access to run docker commands. Only root user has access for now.
## Grant Access to your user to run docker commands
Add the user to the Docker Linux group. Docker group is create by default when docker is installed.
```
sudo usermod -aG docker ubuntu
```
Logout of the session and log back in for the changes to be reflected.
## Verify that Docker is running
Use the same command again, to verify that docker is up and running.
```
docker run hello-world
```
![docker hello](https://github.com/user-attachments/assets/8fbaec52-8dc2-49b2-b302-2ef213ed73d7)
## Clone this repository and move to folder
I have the Dockerfile and app.py in my Github repo.
Dockerfile:
```
FROM ubuntu:latest

# Set the working directory in the image
WORKDIR /app

# Copy the files from the host file system to the image file system
COPY . /app

# Install the necessary packages
RUN apt-get update && apt-get install -y python3 python3-pip

# Set environment variables
ENV NAME World

# Run a command to start the application
CMD ["python3", "app.py"]
```
app.py
```
print("Hello World")
```
Next clone this repo
```
git clone https://github.com/iam-veeramalla/docker-test
cd  first-docker-file
```
## Create a Docker account
https://hub.docker.com/ create an account for yourself.
login to docker in your instance.
```
docker login
```
## Build the first Docker Image
You need to change the username accoringly in the below command
```
docker build -t gagani25/my-first-docker-image:latest .
```
![docker build](https://github.com/user-attachments/assets/4e9165a5-7b7e-4b0f-84af-4d3db9162074)
## Verify Docker Image is created
```
docker images
```
![verify image](https://github.com/user-attachments/assets/7a602a84-581d-46e3-9a04-4ecb86a2c10b)
## Run the First Docker Container
```
docker run -it gagani25/my-first-docker-image
```
Output:
![run](https://github.com/user-attachments/assets/40b2d1fc-587d-4d9e-a9d6-781f3fd8bac1)
## Push the Image to DockerHub
```
docker push gagani25/my-first-docker-image
```
![push terminal](https://github.com/user-attachments/assets/93997c46-8bee-4f82-8def-
f8dd1d81d116)
Now check your repositories in your Docker account. You will see a newly created repo.
![new repo](https://github.com/user-attachments/assets/876a2d1a-faa0-4cda-ba1a-0d4f3545da0e)



