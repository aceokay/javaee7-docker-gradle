### Run Java EE 7 Application as Docker Container using Gradle

This sample application shows how to package a Java EE 7 application as Docker image and run it within a container using [gradle-docker-plugin](https://github.com/bmuschko/gradle-docker-plugin).

1. Create and configure a Docker Machine as explained in [the official Docker installation docs](https://docs.docker.com/engine/installation/).
2. Create a docker-machine by the name of dev, if you don't already have one:
    - `docker-machine create --driver virtualbox default`
    - See [these docs](https://docs.docker.com/machine/get-started/#use-machine-to-run-docker-containers) for more in-depth coverage on creating machines.
2. `gradlew buildImage` to create the Docker Image.
3. `gradlew startContainer` to both create AND run the Docker Container.
4. Access the application at `http://<HOST>:8080/javaee7-docker-gradle/resources/heros`
    -  `<HOST>` can be found as `docker-machine ip <DOCKER MACHINE>`
  
---
### Note on publishing changes:
Perhaps I don't know of the best way yet but you can make changes to any file
 and see resultant changes if you follow along with these instructions:
1. Restart the `dev` machine
    - `docker-machine stop dev`
    - `docker-machine start dev`
2. Rebuild image create container and finally start the new container:
    - `gradle startContainer`
    - Remember, this call creates AND starts the container after a new Image 
is made.

### Notes
After launching the application, here are some fun additional things you can 
do to see what Docker is capable of:
1. See what version of WildFly you're running at `http://<HOST>:8080`
    - Update to a new version of WildFly in the Dockerfile located at src/main/docker and see how quickly it just works.
2. Make changes to the list of heros in the code and see those change after 
republishing a new container. I haven't found a faster way to do this yet...