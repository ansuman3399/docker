# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)


### Docker commands
Docker commands
---------------
To search repos from the host
docker search python:3.6

docker search registry
gives official image of docker registry from docker hub

To filter search results only for Official Images 
docker search --filter "is-official=true" registry

To beautify the results , use --format
docker search --format "table {{.Name}}\t{{.Description}}\t{{.IsOfficial}}" registry

Combined use of --filter and --format ,
docker search --filter "is-official=true" --format "{{.Name}}\n{{.Description}}\n{{.IsOfficial}}" python

to run the docker image in a detached mode(terminal will not be locked for the container) use:
docker run -d -p 5000:5000 ansumanm20/activemq-repo:latest-push 

to run the docker container in attached mode(terminal will be showing logs and will be locked):
docker run -d -p 5000:5000 ansumanm20/activemq-repo:latest-push 

to see the running containers:
docker container ls

to see the logs of a particular container use:
docker logs <container-id>

to see the logs continously(follow the logs):
docker logs -f <container-id>

to remove a container use:
docker container rm <container-id>

to pause a running docker container use:
docker container pause <container-id>

to unpause a container:
docker container unpause <container-id>

to stop a container use:
docker container stop <container-id>

to start a container use:
docker container start <container-id>

to kill a container use:
docker kill <container-id>

NOTE:Stopping a container lets the application to shutdown gracefully whereas killing a container will immediately stop it.

To list the docker images you have in the docker host
docker images
docker image ls

to see the history of an image use:
docker image history <image-name>

To list a particular type of image  say ubuntu in the docker host
docker images ubuntu

Docker Pull -> to pull the specified image from the docker hub to the docker host
docker image pull nginx:latest
this command will pull the nginx image from the docker hub with the "latest" tag.

If you want to pull all the variants of an image , say for nginx
docker image pull --all-tags nginx


--------------------------------------------------------------------
STEPS TO PUSH THE HOST IMAGE INTO THE REPO CREATED IN THE DOCKER HUB
--------------------------------------------------------------------
1.First create a new repo using the docker hub.
Then using the docker client , login into you docker account using the command:
docker login
provide username and password when prompted.

2. After successful login , the local image needs to be tagged to a new image using the following command:
docker tag nginx:latest ansumanmohanty/repos-nginx:cc-latest
where,
"docker tag" is the base command
"nginx:latest" is the host image with tag as latest
"ansumanmohanty" is the host name where the registry is hosted
"/repos-nginx" is the repo name created using the docker hub.
":cc-nginx" is the custom tag that we provided to our newly tagged image.

3.after running the above command , check whether the newly tagged image is listed or not.
docker images
NOTE: The newly created image and the host image that we used to tag/create the new image will have the same IMAGE ID.
This is because docker tag command has created a new alias for your image. So that, the original image will be untouched and all
of its changes can be performed to its aliased image.

4.Now push the newly created image using the command:
docker image push ansumanmohanty/repos-nginx:cc-nginx

----------------------------------------------------------------------

To inspect any image , use inspect
docker image inspect image-name:tag-name

To format the result of the docker inspect command , use --format with the specified format
docker image inspect --format "{{.RepoTags}} : {{.RepoDigests}}" image-name:tag-name
 
To store the configuration details(result of inspect cmd) into a text file for future use :
docker image inspect --format "{{json .config}}" image-name:tagName > file-name.txt 
type ls to check whether the file got generated or not..
to view the content of file use command:
cat filename

To see all the intermediate layers of an image use docker history cmd,
docker image history image-name:tag-name
NOTE: The search command result might have some rows image ID as <Missing> , as the intermediate image id's are given to
 the layers created by dockerfile instructions and they can be used for caching purpose by our own docker host .But , if an image
 is pulled from docker host , such caching might not happen which may cause env conflicts , thats why we are not provided with the
 intermediate image Id's of the pulled images.All we can know is they exists.

To delete an image :
docker image rm image-name:tag-name

To delete an image which is having the same image id , use
docker rmi <image-id> --force

NOTE: START WILL START ANY STOPPED CONTAINERS. 
THIS INCLUDES FRESHLY CREATED CONTAINERS. 
RUN IS A COMBINATION OF CREATE AND START. IT CREATES THE CONTAINER AND STARTS IT.

------------------------------------------
CREATING A CONTAINER
------------------------------------------
To create a container use command : 
docker container create -it --name custom-container-name image-you-want-to-pull:tag-name
Ex: docker container create -it --name doc-busybox-A busybox:latest

where,
"docker container create" is the base command .
"-it" is used to denotes it will be interactive and teletype enabled(Teletype means to start a terminal connection 
  session with the container).
"--name" to name the container
"custom-container-name" the name you want to give the container
"image-you-want-to-pull:tag-name" the image you want to pull from dockerHub and create the container from.

------------------------------------------
RUNNING A CONTAINER
------------------------------------------
To run a container use command
docker container run -itd --name custom-running-container-name image-type-to-run:tag-name
Ex: docker container run -itd --rm --name doc-busybox-B busybox:latest

where,
"docker container run" is the base command
"-itd" used to denote interactive,teletype enabled and detached(to run behind the terminal) mode.
NOTE: Docker container runs in the background of your terminal. It does not receive input or display output. 
If you run containers in the background, you can find out their details using docker ps and then reattach your terminal 
to its input and output.
"--rm" instructs the docker to delete the container after it has finished running.
"--name doc-busybox-B" to name the container
"busybox:latest" is the image you want to run.

-----------------------------------------
To check the running instances of containers use command:
docker ps -a

To check the logs of a particular container
docker logs -f <container-id>

To start a container:
docker container start <container-name>

To stop a running container :
docker container stop <container-name>

To restart a container in a running state:
docker container restart --time 5 <container-name>
 where , "--time 5" indicates a buffer of 5 seconds
 
To rename a container  - even in running state
docker container rename <original-name> <new-name>

To remove a container use:
docker rm container-name

----------------------------------------
EXECUTING COMMAND IN A RUNNING CONTAINER
----------------------------------------

1. Using ATTACH:
docker container attach <container-name>
this means - we are attaching the standard I/O and standard error of the container to the terminal of the docker client.
CONS: if we exit the attached terminal then the running container will be stopped.
So to avoid this we can use EXEC command.

2. Using EXEC:
docker exec -it <container-name> command-to-execute
Ex: docker exec -it busybox-A pwd
This command will execute the pwd command on the container.

----To get a command prompt to execute commands inside the container use:
docker exec -it <container-id> <command>
for eg: docker exec -it 054566561asf sh
insteadof sh you can also use : bash powershell zsh sh
------------------------------------------------------------------
PORT MAPPING ON CONTAINERS : Mapping local port to containers port
------------------------------------------------------------------
To map the container port to the localhost port use:
docker container run -itd --name activemq -p 8161:61616/tcp rmohr/activemq

where,
"docker container run" - to run the container
"-itd" -  to make the container interactive , teletype enabled and run in the detached mode.
"--name" - to name the container
"-p" - to specify port mapping
"8161:61616/tcp" - means mapping the host port 8161 to the container port 61616 on tcp protocol
"rmohr/activemq" - name of the image to run.

-------------------------------------------------------------------------
To remove all the stopped containers:
docker container prune

To remove a stopped container :
docker container rm <container-name>
	or
docker container rm <container-ID>

To remove a running container:
docker container rm <container-id> --force
Note: Better to use	:
docker container kill --signal=SIGTERM <container-name>

--------------------------------------------------
DOCKER NETWORK DRIVERS:

-A piece if software that handles container networking.
-They can be created using docker network command. No images or files are required.
-Responsible for invoking a network inside the host or within the cluster.
-Native network drivers are shipped with docker engine.
-Remote network drivers are created and managed by 3rd party vendors or community.
-Docker also provides IP Address Management(IPAM) drivers , which handles IP address ranges and distribution ,
 if they are not specified by admin

There are 2 types of native network drivers:
1. HOST NETWORK
-Conatiner connected to the host , will have the same IP as that of the host itself.This will not let containers abandon their
 true nature.
-If there are more than 1 containers, then in this case the containers will connect with themselves using the virtual ethernet(VETH),
 reflecting the capabilities and limitation of the host .

2. BRIDGE NETWORK.
-It is the default network for docker containers.
-If we dont explicitly connect our containers to any network, they will be connected to the default bridge network.
-It creates a virtual ethernet bridge.All of the containers connected to this network are connected through this bridge via 
 container endpoints.
-The bridge communicates with the host network, it means the containers will be isolated from the host network specifications.
-Containers will have different IP's than host.
-We can define the Ip range and subnet for the bridge and subsequent networks.
-If we dont define Ip range and subnet fot the netowrk then IPAM drivers will take care for us.

REMOTE NETWORK
-------------
OVERLAY NETWORK
-It is used in clusters mode, like docker swarm.
-Swarm heavily relies on overlay network.	 

--------------------------------------------------
CREATING DOCKER NETWORK
--------------------------------------------------
To create a network driver use:
docker network create --driver bridge my-bridge
where,
"docker network create" is the base command to create a network driver
"--driver bridge" is used to define the type of driver network we are creating , in this case its bridge network.
"my-bridge" is the custom network name.

To create a network driver and specifying the subnet and ip range use:
docker network create --driver bridge --subnet=192.168.0.0/16 --ip-range=192.168.5.0/24 my-bridge-1
where,
"docker network create" is the base command to create a network driver
"--driver bridge" is used to define the type of driver network we are creating , in this case its bridge network.
"my-bridge-1" is the custom network name.
"--subnet=192.168.0.0/16" to privide the subnet of the n/w
"--ip-range=192.168.5.0/24" to proivide the IP range.

To list down the netowrks use:
docker network ls

To filter network search results use:
docker network ls --filter driver=bridge
this will only give the network with bridge type network. 

-------------------------------------------------
CREATING , DISCONNECTING AND INSPECTING NETWORKS
-------------------------------------------------
NOTE: IF WE DONT PROVIDE ANY NETOWRK , THEN DOCKER WILL PROVIDE THE DEFAULT BRIDGE NETWORK TO THE CONTAINER.

In order to connect a network to a container , the container must be running.
Since its an inter-process communication the container should be up , to link it with a network.

To connect a network to a running container use,
docker network connect <network-name> <container-name>

To connect the running container with the host network (Ip same as docker host) use:
docker container run -itd --rm --network host --name <custom-container-name> <image-type-to-run>

To inspect a network use:
docker network inspect <network-name>

-------------------------------------------------
DOCKER VOLUME
-------------------------------------------------
To create a volume:
docker volume create <volume-name>

TO list down the volumes use:
docker volume ls

To list down the volumes which are not monted to any containers use:
docker volume ls --filter "dangling=true"

To inspect  a volume use:
docker volume inspect <volume-name>

To remove a volume(which is not mounted) use:
docker volume rm <volume-name>

NOTE: In order to remove a volume make sure that that the volume is not attached to any containers.
If attached either unmount it or remove the container first and then remove the volume.

MOUNTING VOLUMES TO A CONTAINER
-------------------------------------
To attach a volume to a container use:
docker run -itd --name activemq --volume my-vol:/var/log rmohr/activemq
Here in this command we are running the container with name activemq and attaching the volume my-vol to it 

---------------------------------------------------------------------------------
to see the docker resource usage like disk usage, no of images and container use:
docker system df

to see the docker events(start,stop,kill command) use:
docker system events

to see the stats of a container use:
docker stats <container-id>

while running a container if you want to run it with a specified cpu usage and memory allocation then use:
docker container run -d -p  5000:5000 -m 512m --cpu-quota=50000 ansumanm20/repo-activemq:latest-push
note: total cpu quota available is : 1000000

Build docker image
------------------
Go to the folder and open cmd/powershell where Dockerfile is present
docker build -t ansumanm20/hello-world-python:0.0.1.RELEASE .
where:
-t is for tags
. is for specifying the directory

DOCKER COMPOSE
--------------

after writing the docker-compose.yml file
To run the containers use:
docker-compose up

If you want to build the image because of some changes in the docker-compose.yml file use:
docker-compose up --build

To run the containers in docker-compose in detached mode use:
docker-compose up -d

CONTAINER RESTART POLICY
------------------------
1. "no" - never attempt to restart container if it crashes or stops.
2. "always" - if container stops for any reason always attempt to restart it.
3. "on-failure" - only restart if the container stops with an error code.
4. "unless-stopped" - always restart unless we (the developers) forcibly stopped it.

To run a dockerfile with a custom name say : Dockerfile.dev for dev environment , use:
docker build -f Dockerfile.dev . -t ansumanm20/frontend-react:0.0.1.latest

If you want to see the changes that you make in local to get reflected in the container running(like live server),
then we need to map the volume of the container to the local folder structure like:

docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app <container-id/image-name>
where:
-v /app/node_modules :tells that - dont override the node_modules dir present in the container.
-v $(pwd):/app : maps the /app folder of the container to the local project src folder where code is present ,
 to detect the changes and reflect the same in the browser.
 Note: $(pwd) will not work in windows command prompt or powershell.
 
To run the tests in a node based application , generate the test report and exit automatically use:
docker run ansumanm20/docker-react npm run test -- --coverage
