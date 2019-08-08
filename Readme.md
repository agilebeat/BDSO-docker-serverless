# Environment to build and deploy lambda function 

Use this project to build docker image providing building/deployment
environment for aws lambda function wrapping TensorFlow models.

### Getting Started

First build docker image using the Dockerfile. To build it you have to:

1. Check out this project
2. Get in to the project directory using `cd` command
3. Run 

`docker build . -t aws-serverless-client`

### Running docker

Assuming that you have set up aws client credentials just mount .aws folder
from the host system to the /root/.aws folder in docker container. That
way you don't have to configure it every single time when you run docker
container.

Following example show how to run docker image with mounting folders. In our case
the <PATH-TO-YOUR-SERVERLESS-PROJECT> is the actual lambda serverless project which 
you can check out from github: https://github.com/agilebeat-inc/serverless-lambda-infer-railroad

```
docker run -v <PATH-TO-YOUR-CREDENTIALS-ON-HOST_MACHINE>/.aws:/root/.aws -v <PATH-TO-YOUR-SERVERLESS-PROJECT>:/root/classify-lambda <IMAGE ID>
```

Where:

1. You can get image ID by running following command: 
   
   ```docker image ls```
   
   You should see line 
   
   ```aws-serverless-client latest 0f5875eda9b2 6 days ago 2.55GB```
   
   - aws-serverless-client - is a tag name
   - latest - is version name
   - 0f5875eda9b2 - is the image id
   
If you don't have `aws-serverless-client` image build it.
To build the image just check out this project, get in to directory and run
follwoing command: 

```docker build . -t aws-serverless-client```  
   
### Getting shell for running container

To get shell for running container do:

1. Get running container ID; run command `docker ps`
   
   `CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES`
   `1e0246db6646        0f5875eda9b2        "jupyter notebook --…"   3 days ago          Up 3 days 6006/tcp, 8888/tcp gifted_meitner`
   
2. Get terminal access (shell) by running:

   `docker exec -it <CONTAINER-ID> /bin/bash`

   At this point you should see:
   
   `root@<IMAGE-ID>:/notebooks#`
   
   Comment: Image ID is a static id for an image. When image "runs" it runs in
   a container. So container id is the 'running machine' id 
   
3. Go to home root directory, run:
   
   `cd`
   
4. Check if you see the serverless project folder

   `ls`
   
   You should see folder:
   
   `classify-lambda`