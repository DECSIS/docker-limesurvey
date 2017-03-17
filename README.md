LimeSurvey
==========

Forked from danturner/limesurvey

LimeSurvey - the most popular
Free Open Source Software survey tool on the web.

https://www.limesurvey.org/en/


Containerised version of LimeSurvey that does NOT package Database in the same container. 
Prepared to connect with postgres database


## Usage

To run limesurvey in 80 port just:

    docker run -d --name limesurvey -p 80:80 mmourao/docker-limesurvey:latest

1. Go to a browser and type http://localhost
2. Click Next until you reach the *Database configuration* screen
3. Then enter the following in the field:
  - **Database type** *PostgresSQL*
  - **Database location** *localhost*
  - **Database user** postgres*
  - **Database password**
  - **Database name** *limesurvey* #Or whatever you like
  - **Table prefix** *lime_* #Or whatever you like

You are ready to go.

## Using Docker Compose

You can use docker compose to automate the above command if you create a file called *docker-compose.yml* and put in there the following:

	version: '2'
	services:
	  db:
	    image: 'postgres:9.6.2-alpine'
	    environment:
	      - POSTGRES_PASSWORD=654321
	    expose:
	      - '5432'
	  lime:
	    image: 'mariomourao/docker-limesurvey'
	    links:
	      - db
	    ports:
	      - '80:80'



And run:

    docker-compose up -d