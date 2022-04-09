# Adding-template-to-httpd-image-using-docker

## Description

We are creating an docker container using HTTPD docker image with HTML template. Here we use EC2 instance as our local system and we add docker into that system. Let's move on to the process.

## Installation

If you need to download docker to the EC2 instance, then follow this:

~~~sh
sudo yum install docker -y
sudo systemctl restart docker.service
sudo systemctl enable docker.service
sudo systemctl status docker.service
sudo usermod -a -G docker ec2-user
~~~

Please exit from the instance and login back to reflect the above changes

## Steps involved

## Step 1

Download an sample HTML template to the EC2 instance, you can use this link for getting [sample HTML](https://www.tooplate.com/) . 
Here we downloaded the template to /home/ec2-user/website/ location.

> To get sample HTML template

~~~sh
wget https://www.tooplate.com/zip-templates/2124_vertex.zip /home/ec2-user/website/
cd /home/ec2-user/website/
unzip 2124_vertex.zip
rm -rf 2124_vertex.zip
~~~

![image](https://user-images.githubusercontent.com/100773863/162551874-8a37fd2e-de7f-4737-8b57-0da2c3d47a3e.png)


So, we have the site template in /home/ec2-user/website/


## Step 2

Start a container with HTTPD image, here I use HTTPD image - httpd:2.4-bullseye, you can use this link for getting the [Docker image](https://hub.docker.com/_/httpd) .
In the meantime we use "-v" flag for mounting the current template directory into the container. We also use "-d" flag for running container in detached mode.

~~~sh
docker container run --name webserver -d -p 8080:80 -v /home/ec2-user/website/:/usr/local/apache2/htdocs/ httpd:2.4-bullseye
~~~

We can check the container to make sure the files has been moved/mounted successfully to container using:

~~~sh
docker exec webserver ls -l /usr/local/apache2/htdocs/
~~~

![image](https://user-images.githubusercontent.com/100773863/162551928-745283bd-ca1a-4db4-912b-dab3a546545b.png)

Now the site is active and we can browse it using EC2 IP or hostname.

![image](https://user-images.githubusercontent.com/100773863/162552203-8d75e0cd-8509-4634-b035-efb3fe5e78d3.png)

## Conclusion

This is how an docker container is created with sample HTML teamplate added to docker image. Please contact me when you encounter any difficulty error while using this terrform code. Thank you and have a great day!


### ⚙️ Connect with Me
<p align="center">
<a href="https://www.instagram.com/dev_anand__/"><img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white"/></a>
<a href="https://www.linkedin.com/in/dev-anand-477898201/"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/></a>


















