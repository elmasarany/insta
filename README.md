# Task
## Requirement to build ROR as given in document and convert it to k8s 
* First Issue
it doesn't work as writen in README file of the repo 
i followed the documentation and applied it step by step. 
issue was caused by initializing and migrating database.
```
vi config/db/schema.rb

docker-compose run drkiq rake db:reset

docker-compose run drkiq rake db:migrate
```
it running as well by
```
docker-compose up 
```


## I Run it in EKS 
  * create an EC2 instance and create the EKS by the following steps 
  * install kubectl 
  * create the eks using eksctl 
```

    curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl && chmod +x ./kubectl && mv ./kubectl /usr/local/bin && kubectl version --short --client && sudo mv ./kubectl /usr/local/bin
    
    curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp && sudo mv /tmp/eksctl /usr/local/bin
    
    eksctl create cluster --name instabug    --region us-east-2 --node-type t2.small
```

## convert Docker Compose to k8s
Using Kompose tool [kompose](https://kompose.io/):

## Build Drkiq Image
build Drkiq image and upload it to dockerhub to use it in our deployment file.

## Apply the yaml files 
* Issues happed during the applying 
  
  * Postgres pod crashed and it's happed because following two line was not exis.
```
          name: PGDATA
          value: /var/lib/postgresql/data/pgdata
```
  * Drkiq Pod cann't connected to the Postgres DB 
 Error
 ```
 database "drkiq_development" does not exist
 ```
  i Solve it by creating job to create the Database inside postgres pod.
   
