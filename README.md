# Final project for iTjuana DevOps Bootcamp

## Description
In this project put all the tools learned in the bootcamp in order to create a DevOps process and apply them for automate an app deployment.

## Requirements
* Docker in your machine
* SSH and SSHPASS packages on your machine
* Install Ansible
* Get a GitHub account
* Get a DockerHub account
* Install and update nodeJS and NPM packages

## Guidelines
* Follow the instructions below to get the right results
* Maintain the order of your files and the paths updated
* Get all the requirements before start

## Get the pre-requisites
* Docker installation
  * `Docker --version` show the docker version
* Git installation  
  *`Git --version` show the git version
* Node JS 
  * `npm version` show the node version
* Get the VSC installed

## 1. Setup the environment

### Repository
Firstly, you need to get the link for the forked repository.
* Fork repository: https://github.com/osvaponcee/DevOps.git
* After that, clone it as your local repository:
 * Clone the repository : **`git clone SSH <link_repository>`**

### Application
After, you need to verify the application you will use for this project.
* Go to the folder inside the repository: `/capstone_project/hello-world.`
* Run `npm install`.
* Run `npm test`. Need to pass all the test.
* Run `npm start` This command runs the application.
* Check http://localhost:3000 to verify if the application is running.

## 2. Containerize the application
Using Docker, you will containerize the application in your local repository, starting with Dockerfile and image creation.
* First, you need to go to the path: `capstone_project/hello-world/`. Here is the Dockerfile.
* Put the command: `docker build -t <image_name_you_prefer> .` This command create the image from the Dockerfile.
  * The Dockerfile contains:
  * Works from Ubuntu OS.
  * Install all the necessary packages to work: *ssh, sshpass, nodejs, npm*.
  * Copy all the files into another folder path inside the image.
  * Use `/app/src` as work directory.
  * Install all the dependencies from `package.json` file.
  * Configure the ansible user for the connection.
  * Run the *service ssh start* and the *npm start* commands in order to start the SSH communication and start the application (only applies running the      image.).

After that, you need to run the image, it means build the container using the image as you create before.
* Check if the image was created.
  * `Docker image ls`. This command check all the images on the system.
* Run the command: `Docker run -d -p 3000:3000 --name <container_name_you_prefer> <image_name>`. 
  * This command build the container.
  * The *-d flag* is for running the container as background.
  * The *-p flag* runs the container in an specific port.
  * The *--name flag* allows you to put a name at the container.
* Run the command: `Docker ps -a` to verify if the container was created and is running.
* Then you can go at `http://localhost:3000` in order to check if the application is running.

## 3. Create a CI pipeline 
On this step you'll use the GitHub actions.
* Go to the repository forked and put on the main path.
* Here you have the folder `.github/workflows`. 
* Change the branch at `testworkflows`.
* Go to this folder and here you will see the yaml file.
* Inside this workflow you have two jobs:
  1. The first job have the testing:
    * Here the workflow use the commands from the Application part in order to pass the test again but now on the repository.
  2. The second job have the tasks about Docker:
    * Build the image from the Dockerfile
    * Login into the DockerHub
    * Push the image at the DockerHub

## 4. Update the text from the application using Ansible
Here, you use Ansible to change the text from the application. This works in your local repository.
* First, get the image from DockerHub: `docker pull osvaldoponce01/capstone_project:0.0.1` to get the image on your machine.
* Run the image with the command: `Docker run -d -p 3000:3000 --name <container_name_you_prefer> <image_name>`. To check the current text on the application.
* Then, stop the container with the command: `docker stop <container_name>`.
* Go to the path `capstone_project/hello-world`. Here are all the Ansible files.
* Run the command: `ansible-playbook -i inventory.ini playbook.yaml`. This command runs the playbook and change the text from the App.js.
* Now it's time to update the files, run the command: `docker build -t <image_name_you_prefer> .`. This command allows to update the image.
* Run the command: `Docker run -d -p 3000:3000 --name <container_name_you_prefer> <image_name>`.
* Check the http://localhost:3000 to verify the current text on the application and now you see "Hello Devops!" instead "Hello World!".  








