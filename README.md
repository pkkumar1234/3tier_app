# Docker MySQL Node.js React.js App

![App](https://github.com/prasad0808/3tier_app/blob/main/App.png)

"Docker MySQL Node.js React.js App" is a comprehensive demonstration repository showcasing the capabilities of Docker and Docker Compose. With a focus on simplicity and efficiency, this project illustrates the integration of Docker containers for deploying a full-stack application.

The repository features a React.js frontend application where users can enter their data and submit it. The submitted data is then securely transmitted to a Node.js backend server, which processes and persists it in a MySQL database. By utilizing Docker Compose, the entire application stack, including the frontend, backend, and database, can be effortlessly orchestrated and managed as isolated containers.

## Setup

To set up the project, follow the steps below:

### Prerequisites

Before running the project, make sure you have the following installed:

- Docker: [Download and Install Docker](https://docs.docker.com/get-docker/)

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/prasad0808/3tier_app.git
   ```

2. Navigate to the project directory:

   ```bash
   cd project-directory
   ```

3. Download the `script.sql` file and place it in the project directory.

4. Run the following command to build and start the Docker containers:

   ```bash
   docker-compose up --build
   ```

5. Login to MySQL using the specified port, username, and password:

   - Host: `localhost`
   - Port: `3307`
   - Username: `root`
   - Password: `pass123`

   You can use a MySQL client such as [MySQL Workbench](https://www.mysql.com/products/workbench/) or [phpMyAdmin](https://www.phpmyadmin.net/) to log in to the MySQL server.

6. Initialize the MySQL database by executing the `script.sql` file.

7. Access the application by opening the following URL in your web browser:

   ```
   http://localhost:3001
   ```

   This will take you to the ReactJS application interface where you can interact with the project.

   ## Usage

This example serves as a beginner-friendly resource to learn about full-stack Docker containerization in a practical application. It provides a simplified implementation of a full-stack application using React.js, Node.js, and MySQL, all orchestrated with Docker Compose.


#############################################################################################################################

##Deploy node application using dockerfile and commandline

1. Create ec2 instance and launch
2. Install docker
     - apt install docker.io 
4. Give docker permission
     - usermod -aG docker $USER
6. - newgrp docker
4. Allow port for frontend-(3001) and backend-(3000)
5. Clone repo from github
    - https://github.com/pkkumar1234/3tier_app.git
7. Go to frontend directory and inside src folder in App.js file open and change
   
    - const URL = "http://<your-ip-address>:3000";
   
8. Create image for frontend
     - docker build -t front-img .
10. Go to backend directory and create image for backend
      - docker build -t backend-img . 
12. Create network
      - docker network create mynetwork 
14. Run frontend container
      - docker run -d –name front-con -p 3001:3000 image-name 
16. Attach frontend container to network
      - docker network connect mynetwork container-name
18. Pull and run image container mysql and give some credential
    
             docker run -d \
              --name db \
              --network mynetwork \
              -e MYSQL_PASSWORD=pass123 \
              -e MYSQL_ROOT_PASSWORD=pass123 \
              -e MYSQL_DATABASE=appdb \
              -p 3306:3306 \
              mysql
    
19. Run backend network and add with credential  
                docker run -d \
                 --name backend-con \
                 --network mynetwork \
                 -e DB_HOST=db \
                 -e DB_USER=root \
                 -e DB_PASSWORD=pass123 \
                 -e DB_NAME=appdb \
                 -p 3000:3000 \
                 App-backend
14. Go to mysql container dump script.sql or manually create table
            USE appdb;
            
            -- Create the apptb table
            CREATE TABLE `appdb`.`apptb` (
              `id` INT NOT NULL AUTO_INCREMENT,
              `name` VARCHAR(45) NOT NULL,
              PRIMARY KEY (`id`));

15. After restart container
    - docker restart container-name 

   

