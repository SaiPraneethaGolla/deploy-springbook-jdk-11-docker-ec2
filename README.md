# deploy-springbook-jdk-11-docker-ec2
########################## UPDATE LINUX PACKAGES ###################

1) sudo yum update -y

########################## INSTALL JAVA-jdk-11 ###################

1) sudo amazon-linux-extras install java-openjdk11 -y

########################## INSTALL MAVEN ###################

1) sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo

2) sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo

3) sudo yum install  apache-maven -y

4) sudo update-alternatives --config java #pick java 11       

5) mvn --version

########################## INSTALL DOCKER ###################

1) sudo yum update -y

2) sudo amazon-linux-extras install docker -y

3) sudo service docker start

4) sudo systemctl enable docker

5) sudo setfacl -m user:ec2-user:rw /var/run/docker.sock

6) sudo usermod -a -G docker ec2-user


########################## INSTALL GIT ###################

1) sudo yum install git -y

########################## CLONE GIT REPOSITORY ###################

1) git clone https://github.com/Uppala-Naveen-Goud/BackendServer.git (Clone git repository into local machine)

2) cd BackendServer ( Change directory into project folder)


########################## RUN JAVA APPLICATION USING DOCKER  ###################

1) mvn clean install (To build Java application. Jar file will be created)

2) docker build -f Dockerfile -t springboot . (Build docker image using Dockerfile in project folder)

3) docker run -it --name container_name -p 8081:8081 image_name (Run the docker Image by giving the container name, port number and specifying the Image name at the end)


########################## STOP JAVA APPLICATION ###################
1) docker stop container_name  ( To stop running spring boot application)

##########################Export Logs to CloudWatch #######################

1) docker run  -d --name container_name   --log-driver=awslogs  --log-opt awslogs-region=ap-south-1  --log-opt awslogs-group=Backend  --log-opt awslogs-create-group=true -p 8081:8081 image_name
