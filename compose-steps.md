# Docker Compose
- Docker Compose is a tool for defining and running multi-container applications.
- It is the key to unlocking a streamlined and efficient development and deployment experience.
- Compose simplifies the control of your entire application stack, making it easy to manage services, networks, and volumes in a single YAML configuration file.
- Then, with a single command, you create and start all the services from your configuration file.


## Create Database In RDS 

**Go To RDS**
- Created Database
- Standard create
- choose template as Free tier
- DB name – database-1
- Username – admin
- Password – Passwd123$
- VPC – VPC-3-tier
- Connect to Instance -> choose database instance
- create security group
**Create database**

  ### $$\color{orange} \textbf {Now SSH  into Database  Server}$$

![database-instance](https://github.com/abhipraydhoble/Project-3-tier-Student-App/assets/122669982/8159a278-d612-441e-93da-d581428cdd3a)

````
sudo apt update -y
````
````
sudo  apt install mariadb-server -y
````
````
systemctl start mariadb
````
````
systemctl enable mariadb
````
### $\color{orange} \textbf{Log \ in \ into \ database}$

![login into database](https://github.com/abhipraydhoble/Project-3-tier-Student-App/assets/122669982/ba0c082a-060f-48f9-8520-83c906337251)

````
mysql -h rds-endpoint   -u admin -pPasswd123$
````
Note: replace rds-endpoint with actual endpoint value

````
show databases;
````
````
create database  studentapp;
````
````
use studentapp;
````

### $\color{blue} \textbf{Run \ this \ query \ to \ create \ table:}$
````
 CREATE TABLE if not exists students(student_id INT NOT NULL AUTO_INCREMENT,  
	student_name VARCHAR(100) NOT NULL,  
	student_addr VARCHAR(100) NOT NULL,   
	student_age VARCHAR(3) NOT NULL,      
	student_qual VARCHAR(20) NOT NULL,     
	student_percent VARCHAR(10) NOT NULL,   
	student_year_passed VARCHAR(10) NOT NULL,  
	PRIMARY KEY (student_id)  
);
````
````
show tables;
````
Logout from database:
````
exit
````
---
# docker-compose installation

````
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d'"' -f4)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
````
````
sudo chmod +x /usr/local/bin/docker-compose
````
````
docker-compose --version
````
## clone repository
````
git clone https://github.com/abhipraydhoble/ThreeTier-Using-Docker.git
cd ThreeTier-Using-Docker
````
## add connection string in ./Backend/context.xml 
## add instance ip ./Frontend/index.html

### docker compose commands
````
vim docker-compose.yaml
````
- add environment values
  
````
docker-compose build
````
````
docker-compose up -d
````
````
docker-compose down
````
