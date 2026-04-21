## 5.4 Reflection 

### How can you check logs from a running container?
- 'docker logs containerID' command does exactly that. 

### What is the difference between docker exec and docker attach?
- docker attach connects directly to the running app process. You can watch or interact with the app while its live. docker exec opens a seperate terminal inside the running container. This lets you use terminal commands, inspect, debug and test the connection of the application. 

### How do you restart a container without losing data?
- You need to use docker volumes, that will store all the data outside of the containers either locally or in the cloud depending on the data. 

### How can you troubleshoot database connection issues inside a containerized NestJS app?
- First check if both postgresql and nestjs containers are running. Then check the logs to find any errors related to the database. You can also enter nestJS container and test the database connection from inside. 
- use docker ps, docker logs, docker exec -it 