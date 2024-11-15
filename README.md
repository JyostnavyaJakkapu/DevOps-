# STEP1 : Docker Installation

 1: This setion guides through the Docker Desktop installation on your machine. Please follow the offical documentation link to install https://docs.docker.com/engine/install/

 2: After installation, restart the machine then open Docker Desktop application.

 3: Check the version of Docker by launching the terminal, if you are on commandprompt for Windows or terminal for Mac and for other OS launch up the shell--> 
 
 `docker --version` 
 


# STEP 2 : DEVOPS USE CASES

Consider you are a part of DevOps teams working on the amazing project, building APIs in Java, Python, JavaScript. You are ready with the basic versions of all these applications, and you would like to deploy them quickly to the QA environment, also you have a new team member pairing up with you who wants to understand how to deploy applications to QA. So you both sit at a desk Launch up terminal and ready to execute few commands. If you are on Mac, launch terminal, on Windows launch command prompt and on other OS launch Shell.

`docker --version`

# STEP 3 : DOCKER CONTAINERS

`docker run -p 5000:5000 jyostnavyajakkapu/hello-world-python:0.0.1.RELEASE`

# command explaination 

--> jyostnavyajakkapu/hello-world-python:0.0.1.RELEASE --> path to the docker image which is stored on the docker registry called docker hub

--> Docker Hub is public docker registery which is accessible at https://hub.docker.com/. Docker Registery contains a lot of different repositories of different versions of differnt applications.

--> When we specify the path to the image, wespecify 2 things:

1. jyostnavyajakkapu/hello-world-python --> Docker Repository

2. 0.0.1.RELEASE--> Specific tag, this specific image contains everything that we need to run the specific application, it contains all the releases like right software to run your application need,libraries and also the dependencies.

** Static version of the image "jyostnavyajakkapu/hello-world-python:0.0.1.RELEASE"on the repository or local machine-- image

--> running version of this image "jyostnavyajakkapu/hello-world-python:0.0.1.RELEASE"--container **

*NOTE* 

For one image, we have a lot of containers which are running

1.  -p 5000:5000 --> Whenever we run a container, it is a part of internal network called Bridge by default all the containers run inside the bridge network.
2. Containers cannot be accessed unless the port is exposed, consider the scenario here 5000:5000, the container port 5000(right side) is mapped to host port(left side) and option which enable us to do this is -p, short cut for --publish

# STEP 4 : MULTIPLE INSTANCES OF THE SAME APPLICATION RUNNING

 --> `docker run -p 5000:5000 jyostnavyajakkapu/hello-world-python:0.0.1.RELEASE`

 -->`docker run -p 5001:5000 jyostnavyajakkapu/hello-world-python:0.0.1.RELEASE  // Running the application on different ports`
  
 --> `docker run -p 5003:5000 jyostnavyajakkapu/hello-world-java:0.0.1.RELEASE`

  -->`docker run -p 5004:5000 jyostnavyajakkapu/hello-world-nodejs:0.0.1.RELEASE `

*NOTE*

Once you have a docker image, it doesnot matter whether it is image of python or java or nodejs application, you can run it in the same way

# STEP 5 : DETACHED MODE AND LOGS

i. Launch up the container in detached mode ---> `docker run -d -p 5000:5000 jyostnavyajakkapu/hello-world-nodejs:0.0.1.RELEASE`

ii. command to check the logs --> `docker logs container_id`

iii. command to follow the logs with specific application  --> `docker logs -f container_id`

# STEP 6 : DOCKER IMAGES AND CONTAINERS

-->`docker images` //displays the list of images

-->`docker container ls` //displays the list of running containers

-->`docker container ls -a` //displays the list of all containers including the exited containers

-->`docker container stop container_id` // stops the container

# STEP 7 : UNDERSTANDING DOCKER POPULARITY -- TOP 3 REASONS 

1. Standardized Application Packaging - Same packaging for all types of application either java or python or JavaScript, you would build the docker image

2. Multi Platform Support - Once the docker engine is installed, we can run the created docker images anywhere either on Local machines, data center, Cloud - AWS, Azure, GCP

3. Light-weight Support - Containers are light- weight as compared to VM's, Isolate from one another

--> Before the era of Docker, we can virtualize something with the help of Virtualization

(Refer deployments using Virtual Machines diagram -- layers are hardware, Host OS, Hyperviso, Guest OS, Software and application )

. With Virtual Machines, there are 2 Operating systems i.e., Host OS and Guest OS because of which VM's are heavy weight. When we virtualize , we may not be able to use the entire power of hardware because of virtualization, now docker comes into picture.

Refer to  Deployment using Docker - consists of layers such as Cloud Infrastructure, Host OS, Docker Engine, Containers.

# STEP 8: DOCKER IMAGES - COMMANDS

`docker images`  // displays all the images

`docker pull mysql` // only pulls the images but will not run the container for it 

`docker search mysql`  //To find out the different images present in the docker registry -- look for the official images

--> Docker images are built in number of layers - layer with OS, layer with software, layer with Specification binary , to see the layers inside the image

    docker image history jyostnavyajakkapu/hello-world-java:0.0.1.RELEASE --> //jyostnavyajakkapu/hello-world-java is the repository name and 0.0.1.RELEASE is the tag name

                OR

    docker image history image_id

--> Details behind each of the images can be checked using docker inspect commmand

    docker image inspect image_id

--> Removing the images on the docker -- to remove an image there should not be any running containers or stopped containers

    docker image remove mysql // remove the image immeadiately as there is no existing container for pulled images, basically it removes the image from the local machine not the docker hub

                            or

    If there is a running container, we have stop the container using the command "docker container stop container_id"  then only we can remove the container first by using the command "docker container rm container_id" 
    
    then try removing the image by using the command :

    docker image remove image_id (or) docker image remove jyostnavyajakkapu/hello-world-java:0.0.1.RELEASE

# STEP 9 : LEARNING DOCKER CONTAINERS --COMMANDS 

--> `docker run -d -p 5000:5000 nginx` is the shortcut for the command `docker container run -d -p 5000:5000 nginx` // in detached mode, containers will be created and are upend running

--> `docker container ls` // shows the running containers

--> `docker container ls -a` //shows all the containers regardless of whether it is running container or exited container

--> `docker container pause container_id`  //pauses the container -- In this stage, the container will not serve any request, if we refresh -- it will just hang without any output

--> `docker container unpause container_id`  //unpauses the container, once refreshed -- we can see output on the port assigned

# STEP 10 : DIFFERENCE BETWEEN DOCKER CONTAINER STOP AND DOCKER CONTAINER KILL

--> `docker run -d -p 5000:5000 nginx`

--> `docker container stop container_id`  // allows some time to shutdown the application gracefully. In technical terms, we are sending a signal to the container called sigterm

--> `docker container logs -f container_id`  //checks the logs of the container

--> `docker container kill container _id`  // doesnot give time to shutdown the application gracefully. In technical terms, when we are killing the container --the signal we are sending to a container called sigkill means stop everything and drop there 

-->`docker container inspect container_id` // holds the details of the container

-->`docker container prune`  // removes all the stopped containers

# STEP 11 : Learning Docker commands - system and stats 

--> `docker system df` // shows the docker disk usage

--> `docker system events` // shows the commands which are running on the container

--> `docker system prune -a` //deletes all the stooped containers and all the images without the atlease 1 container associated with it, also removes the network not used by atleast 1 container and build cache

--> `docker system info` //displays the system wide information

--> `docker stats container_id` //shows the stats of that particular container_id including how much memory, CPU is used

--> `docker container run -d -p 5000:5000 -m 6m --cpu-quota=50000 bitnami/java` //once the application starts, reduces the cpu utilization and memory

# STEP 12 : Building Docker images for Python application

--> `cd directory`

--> `docker build -t repository_name:tag_name .` // builds the image tagged to specific --build context is sent to docker daemon and shows the step by step installation

--> `docker run -p -d host_port:container_port repository_name:tag_name`  //creates the container 

--> `docker logs -f container_id` // check the logs whether the container is upend running then check on the local host .

# STEP 13 : PUSHING PYTHON APP DOCKER IMAGES TO DOCKER HUB

--> `mkdir my-python-app`

--> `cd my-python-app`

--> `touch Dockerfile`

--> `vi Dockerfile`  Press i to insert data and :wq to write and quit 

add requirements.txt and app.py files to the folder

requirements.txt

flask
requests

app.py

# app.py

from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, Docker!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)


--> `docker build -t <docker-hub-username>/my-python-app:latest .`

--> `docker run -p 5000:5000 <docker-hub-username>/my-python-app:latest`

Once the image is created, we can push the image to docker hub

1. `docker login`

2. `docker push <docker-username>/my-python-app:latest`

3. Once the iamges is pushed, refresh the docker hub and you can see the docker image on docker hub

# STEP 14: BUILDING EFFICIENT DOCKER IMAGES - IMPROVING LAYER CACHING

Layers are cached, which makes it fast to build the docker image and push the image to he docker hub and pull the image to wherever you want to deploy it.

# STEP 15 : UNDERSTANDING ENTRYPOINT VS CMD 

With CMD, whatever you pass through the command line will replace with the instructions you will execute and the application will not launch up. 

However with ENTRYPOINT, doesnot worry about command line arguments -- static

Overriding in ENTRYPOINT is much more complex and can be done with the command ` docker run -d -p --entrypoint = "" 5000:5000 jyostnavyajakkapu/my-hello-world:0.0.1.RELEASE`

# STEP 16:DOCKER AND MICRO-SERVICES

# Microservices 

1. REST

2.  & Small well chosen deployable units

3.  & Cloud Enabled

# Advantages of Microservices Architecture:

1. Enables to adapt new technology & processes very easily

2. Dynamic scaling -- for example amazon, they dont have the same load like hugh amount on festive season and less load during the normal day so if microservices are cloud then they can be scaled dynamically and you can procure hardware and release it dynamically

3. Faster release cycles

# Docker makes the life easier with microservices:

1. Easy development
   i. Adapts new technology and process -- zero worry about deployment issues
   ii. Fewer environment issues -- No more "It works in the local"

2. Easier operations :  Consistent deployment automation across different environments and differnet technologies

# STEP 17 : Using link to connnect microservices

1. Build the images for currncy_exchange `docker build -t jyostnavyajakkapu/currency-exchange:0.0.1-RELEASE .` and currency_conversion `docker build -t jyostnavyajakkapu/currency-conversion:0.0.1-RELEASE .`

2. `docker run -d -p 8100:8100 --name=currency-conversion jyostnavyajakkapu/currency-conversion:0.0.1-RELEASE`

3. Remove the currency-conversion container using the command " docker container stop container_id " 
 `docker run -d -p 8100:8100 --env CURRENCY_EXCHANGE_SERVICE_HOST=http://currency-exchange --name=currency-conversion --link currency-exchange jyostnavyajakkapu/currency-conversion:0.0.1-RELEASE`

# STEP 18 : Using Custom Networking to connect microservices

--> `docker network create currency-network`

--> `docker container stop currency-exchange`

--> `docker container stop currency-conversion`

--> `docker rm currency-exchange`

--> `docker rm currency-conversion`

--> `docker run -d -p 8000:8000 --name=currency-exchange --network=currency-network jyostnavyajakkapu/currency-exchange:0.0.1-RELEASE`

--> `docker run -d -p 8100:8100 --env CURRENCY_EXCHANGE_SERVICE_HOST=http://currency-exchange --name=currency-conversion --network=currency-network jyostnavyajakkapu/currency-conversion:0.0.1-RELEASE`

# STEP 19: Using docker compose to simplify Microservices Launch

--> `docker container stop currency-exchange`

--> `docker container stop currency-conversion`

--> `cd current_directory` 

--> `docker-compose up`

--> `docker-compose up -d` //launches the containers in detached mode

--> `docker container ls` // shows 2 containers

--> `docker network ls` //shows all the networks created including the microservices_currency-compose-network which is created by docker compose where in microservices is the name of the folder and currency-compose-network is the name of the network 

--> `docker network inspect microservices_currency-compose-network`

--> `docker-compose down` //stops the running containers

--> `docker-compose events` //shows all the events happenning

--> `docker-compose config` // shows the configuration which is used to launch the docker compose.Used to validate the yaml file 

--> `docker-compose images` // shows the list of images which are used by docker compose

--> `docker-compose ps` //lists downs the containers

--> `docker-compose top` //gives the top process which are running in each of the container

--> `docker-compose pause`

--> `docker-compose unpause`

--> `docker-compose stop`

--> `docker-compose kill`



   








