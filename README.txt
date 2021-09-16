Welcome to Dockerizing Spring boot Java App!!!!!

follow below steps for building Docker images and running Docker containers from images
Pre-requistes:
Make sure you open port 8085 in security firewall. 
also install Java and Maven.


Steps:

1. Make sure you clone the repo locally.

git clone https://bitbucket.org/ananthkannan/myawesomeangularapprepo

2. once cloned, navigate to repo folder
cd ~/myawesomeangularapprepo/MyAwesomeApp/

3. now run the maven build to make sure you are able to build springboot Jar
sudo apt install maven

mvn clean install

4.once you are able build springboot Jar, next step is build docker images

sudo docker build . -t change_to_your_docker_user_id/myspringbootapp 

(make sure you change per your username

5. verify by you have built images successfully
sudo docker images

REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
change_to_your_docker_user_id/springbootapp   latest              69c91142dca6        13 minutes ago      302MB

6. Now run the Docker container from the Docker image you built
sudo docker run -p 8085:8085 change_to_your_docker_user_id/myspringbootapp

7. Now go to browser, and access public DNS name with port 8085
you should see the springboot web app page running
