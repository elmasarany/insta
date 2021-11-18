# Task
## Requirement to build ROR as given in document and convert it to k8s 
* First Issue
it doesn't work as writen in read mefile of the repo 
i had follow the documentation and apply it step by step 
issue caused by initializing and migrate database.
```
vi config/db/schema.rb

docker-compose run drkiq rake db:reset

docker-compose run drkiq rake db:migrate
```
it running as well by
```
docker-compose up 
```
* Second issue 

i don't have k8s on my machine so i decide to Run it in EKS 
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

## Apply the yaml files 
  ## issues displayied during the applying
  * Postgres pod crashed and it's happed because 
```
          name: PGDATA
          value: /var/lib/postgresql/data/pgdata
```          
