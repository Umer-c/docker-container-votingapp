# docker-container-votingapp
Running a micro-service on docker container 

I am going to use the sample code available at "https://github.com/dockersamples/example-voting-app", to run a micro service on docker container.
The overview of the service is as depicted in the diagram below:

<img width="823" alt="image" src="https://github.com/user-attachments/assets/c29bffdc-0861-4037-87c5-0290a9aac98e">

I have already created the images using the Dockerfile available in the example repo and pushed the images to my docker hub account.
Using the configuration in the docker-compose.yml file, we can bring up the 5 container, running each service.
Sample is as below:

```
version: "3"

services:

  redis:
    image: redis

  db:
    image: postgres:9.4
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres

  vote:
    image: umasghar/voting-app
    ports:
      - 5050:80

  worker:
    image: umasghar/worker-app

  result:
    image: umasghar/result-app
    ports:
      - 5001:80

```

Once the file is ready we can simply use the following command to bring up the containers and test the app.

```
docker compose up -d
```

The voting app can be accessed at localhost:5050:

<img width="973" alt="image" src="https://github.com/user-attachments/assets/76784ac5-3c01-4092-84bb-cd1a1ca6889d">

The result app at localhost:5001:

<img width="1007" alt="image" src="https://github.com/user-attachments/assets/8d489f18-fd74-4d01-913e-d7a6198256d6">

