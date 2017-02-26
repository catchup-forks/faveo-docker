<h3>Docker file for Faveo HELPDESK</h3>

With this Docker file you can build a Docker image for Faveo HELPDESK

<h3>How to use</h3>

Clone the repository. 

Make sure you have docker-compose installed on your server. 

Run the following command to start Faveo and mySQL image:

<code>docker-compose up -d</code>

Open you ip address for fininshing Faveo installation.

When asked about database config. Use the same credentials as in docker-compose.yml:

       MYSQL_ROOT_PASSWORD: faveo
       MYSQL_DATABASE: faveo
       MYSQL_USER: faveo
       MYSQL_PASSWORD: faveo

You can change the environment variables for database configuration.

<h3>To change the nginx config image for your server edit defaul.config</h3>

After changing nginx config rebuild the image.

<code>docker build -it "repo_name" .</code>

Now start the server using your own local image by changing the docker-compose file with your repo name as image under faveo:

version: '2'

services:
   mysql:
     image: mysql:latest
     container_name: mysql
     restart: always
     volumes:
       - db_data:/var/lib/mysql
     environment:
       MYSQL_ROOT_PASSWORD: faveo
       MYSQL_DATABASE: faveo
       MYSQL_USER: faveo
       MYSQL_PASSWORD: faveo
     ports:
       - "3306:3306"

   faveo:
     container_name: faveo
     depends_on:
       - mysql
     image: "repo_name"
     ports:
       - "80:80"
     restart: always


volumes:
    db_data:




