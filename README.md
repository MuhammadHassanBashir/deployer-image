I have ran this in cloud run by containizating this the terraform file. Below are the step which i followed

- Create terraform files (main.tf or variable.tf)
- Create bash script for automating the execution of terraform file name terraform.sh
- After that i had create the dockerfile using these file name Dockerfile.terraform, Build and push image to the GCR. So i can run this in cloudrun as job.
- I have passed all variable for terrform from cloud run section. Because i am using terraform.sh which is basically a script, so we can get variable outside the script using "$" sign.. I have use this with terraform plan and apply command. this will give priorty to the variable and main this to main.tf


Now in a same why, I am running the same deployer image in kubernetes as job. 

- I have a image, and i would create helm chart to this job and pass variables using values.yaml

And because, i need to deploy this through GCP market place. 

- i would pass variable to values.yaml through GCP market place schema.yaml file.
