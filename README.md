# cmpe273-lab1
The purpose of this repo is to setup a Docker enviroment.

Pre-requisites

Install Visual Studio Code with Python extension.
A Github Account
A Linux Bash Shell
Windows 10's Bash Shell
Cygwin for older Windows

Steps

[1] Install Docker
[2] Create a Github repo called "cmpe273-lab1" and clone the repo to your local machine.
git clone https://github.com/{your_username}/cmpe273-lab1
cd cmpe273-lab1
[3] Create requirements.txt file and add this line to the file.
flask
[4] Create a Python script app.py file and add these code to the file.
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello from Dockerized Flask App!!"

if __name__ == "__main__":
    app.run(debug=True,host='0.0.0.0')
[5] Create a Docker file Dockerfile without any file extension and add these lines to the file.
FROM python:3.5.2
MAINTAINER Your Name "yourname@gmail.com"
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["app.py"]
[6] Run this command inside the cmpe273-lab1 working directory. Make sure you have all these files in the current directory: Dockerfile, app.py, and requirements.txt
docker build -t lab1-flask-app:latest .
[7] Run this Docker command to list all images.
docker images
[8] Run the Docker container using the image you created in the previous step.
docker run -d -p 5000:5000 lab1-flask-app
[9] Lookup IP of the Lab1-flask-app container.
docker-machine ls
# OR 
docker-machine ip default
NAME      ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER    ERRORS
default   *        virtualbox   Running   tcp://192.168.99.100:2376           v1.11.1   
tester    -        virtualbox   Saved                                         Unknown   
Example: Under the "URL" column, "192.168.99.100" is the IP of your container.
[10] Open this URL in a web browser. If you see the Hello message, you can now commit all three files into your Github repo (cmpe273-lab1).
http://{IP_FROM_STEP_9}:5000/
