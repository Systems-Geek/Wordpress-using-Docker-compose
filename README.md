Setting Up WordPress with Docker Compose

This tutorial guides you through the process of setting up a WordPress environment using Docker Compose. Docker Compose is a tool that simplifies the process of defining and running multi-container Docker applications.

Step 1: Install Docker and Docker Compose

# sudo apt install apt-transport-https ca-certificates curl software-properties-common

 # curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg # echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null 

# sudo apt update 

# sudo apt install docker-ce docker-ce-cli containerd.io

 

Install Docker Compose

# sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# sudo chmod +x /usr/local/bin/docker-compose

 
Step 2: Set Up a Project Directory

# mkdir wordpress-project
# cd wordpress-project
Step 3: Create a Docker Compose YAML file
Use this test config if you want:

version: '3'
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: your_mysql_root_password
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
   MYSQL_PASSWORD: your_mysql_password

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - 8000:80
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: your_mysql_password
volumes:
  db_data: {}

Step 4: Start the Docker Containers

# docker-compose up –d


Step 5: Access Your WordPress Site

You can access your WordPress site once the containers are up and running by opening a web browser and typing http://servers-IP:8000 into the address bar.

Step 6: Complete the WordPress Setup
 

Step 7: Stop and Start Containers

To stop the running containers, use the following command:
 # docker-compose down

