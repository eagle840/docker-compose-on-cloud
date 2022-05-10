# Docker compose and fargate
## docker_compose_fargate

An overview of using a docker compose file on Fargate (This will also work with Azure ACI containers).
This is a simplified instruction taked from: [AWS Blog](https://aws.amazon.com/blogs/containers/deploy-applications-on-amazon-ecs-using-docker-compose/) and [Docker docs](https://docs.docker.com/cloud/ecs-integration/) and the Github [repo](https://github.com/mreferre/yelb) for the AWS blog.

For Windows:
 requirements:
  - AWS account and AWSCLI client installed (choco install awscli)
  - Docker Desktop for Windows
  - Basic understanding of AWS (or Azure) and Docker Compose
  - for Azure ACI see [ACI-Integration](https://docs.docker.com/cloud/aci-integration/)
  - AWS policy permissions maybe required, depending on the account uses- see [Docker docs](https://docs.docker.com/cloud/ecs-integration/)
  
  
# Docker Compose and Context

There is a shift over from the old 'docker-compose' command to the new 'docker compose' be sure to use the new version of the command to use with Fargate.

Then Docker is installed there is a 'context' that is set up to work with the local Docker Daemon (default). Running  
***'docker context list'***   
will show you the available contexts. To select a context, you can use the 'docker context use <name>'
  
Before you setup AWS ECS, be sure to install the awscli, and the set the AWS config, then run the following command:
  
  ***'docker context create ecs myecscontext'***
  
you'll prompted to enter the AWS credientals - in this case use 'AWS environment variables'
  
Now using the docker-compose file provided, run 
  
  ***'docker compose up'***
  
To discover the public endpoint that AWS has given you for the container, run 'docker compose ps', 
 
Once you have finish, just destroy your stack, run:
 
 ***'docker compose down'**
 
Then return you docker context to default
 
 ***'docker context use default'***
    
## issues
  
  - docker build commands in a docker-compose file won't run
  - does the awscli need to be installed - just provide the credentials
  - deployment will fail if the github repo name used does not follow the:    ValidationError: 1 validation error detected: Value 'docker_compose_fargate' at 'stackName' failed to satisfy constraint: Member must satisfy regular expression pattern: [a-zA-Z][-a-zA-Z0-9]*
  - update with linux version, using https://docs.docker.com/cloud/ecs-integration/#install-the-docker-compose-cli-on-linux
 
  
