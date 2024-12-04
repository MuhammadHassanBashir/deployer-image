I have ran this in cloud run by containizating this the terraform file. Below are the step which i followed

- Create terraform files (main.tf or variable.tf)
- Create bash script for automating the execution of terraform file name terraform.sh
- After that i had create the dockerfile using these file name Dockerfile.terraform, Build and push image to the GCR. So i can run this in cloudrun as job.
- I have passed all variable for terrform from cloud run section. Because i am using terraform.sh which is basically a script, so we can get variable outside the script using "$" sign.. I have use this with terraform plan and apply command. this will give priorty to the variable and main this to main.tf


Now in a same why, I am running the same deployer image in kubernetes as job. 

- I have a image, and i would create helm chart to this job and pass variables using values.yaml

And because, i need to deploy this through GCP market place. 

- i would pass variable to values.yaml through GCP market place schema.yaml file.


## REMEMBER: There are multiple ways of assigning the variables to different dev Ops tools\

like:
----

- If you are running terraform locally with terraform init and plan, apply command, **then you can pass variables through variable.tf or you can define variable on  variable.tfvar file and .tfvar file passing that variable to variable.tf but during executing terraform plan and terraform apply you need to select .tfvar file for variable. so terraform will get to know that variable are define in .tfvar file and terraform will pass these variable to main.tf** or you can also pass variable by running **terraform plan -vars=name=values flags and terraform apply -vars=name=values  flag** it will take the most precidence. 

- if you are defining terraform plan -vars= and terraform apply -vars= command in bash file for making it automate, and want to get values outside the bash file.. when you can use "$" sign with value.

  like this:

  !#/bin/bash
  terraform plan -vars="project-id=$project-id" 
  terraform apply -vars="project-id=$project-id"

  You also need to export enviroment variable on terminal using "export" command. where you going to run bash file.

  like this:
  ---------

  export project-id=values of project id   

  once terraform run plan and apply command , it will get the variable values from terminal what you have give during using export command..

- if you are trying to run this with docker, then you can use **-e** flag with docker run command for passing environment variable to docker container

   like this:
   ---------
    docker run \
      -e PROJECT_ID="world-learning-400909" \
      -e PROJECT_NUMBER="22927148231" \
      -e DEFAULT_OWNER_EMAIL="muhammadhassanb122@gmail.com" \
      -e REGION="us-central1" \
      -e LOCATION="us-central1-c" \
      -e VPC_NAME="uscentral-vpc01-100008" \
      -e SUBNET_NAME="uscentral-disearch-vpc01-subnet1000024" \
      -e GKE_SUBNET_NAME="uscentral-disearch-vpc01-subnet1010016-gke" \
      -e DB_INSTANCE_DISK_SIZE="20" \
      -e DB_USERNAME="postgres" \
      -e DB_PASSWORD="CKhEJZH[uFS;%=Mg8iwueVm&x" \
      -e CLOUD_RUN_SERVICE_NAME="my-cloud-run-service" \
      -e GKE_CLUSTER_NAME="disearch-cluster" \
      -e GKE_NODES_MACHINE_TYPE="e2-highmem-4" \
      -e STORAGE_BUCKET_NAME="disearch-storage-bucket" \
      -e STRIPE_SECRET_KEY="" \
      -e ARETEC_ADMIN="secret123" \
      -e LOGS_URL="http://ipaddress:24224/myapp.logs" \
      -e OPENAI_KEY="" \
      -e OPENAI_API_KEY="" \
      -e SERVICE_ACCOUNT_KEY='{service account }' \
     -itd gcr.io/aretecinc-public/disearch/deployer/terraform-deployer:latest
    

- You can pass enviroment variable to kubernetes pod through "configmap" and "secret" as env.  and you application  or bash will get these variables from env.   
  
  

  
  
