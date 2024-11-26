DNS NAME
S3 BUCKET 
IAM ROLE AND ASSIGN IT TO EC2 
CREATE A EC2 INSTANCE AND GENERATE SSH ROLE
download Kops and Kubectl to usr/local/bin and change permissions.

# Download Kubectl and give permissions.
# edit .bashrc and add all the env variables 

 ``` bash
export NAME=pramothdevops.xyz
export KOPS_STATE_STORE=s3://pramothdevopsxyz
export AWS_REGION=us-east-1
export CLUSTER_NAME=pramothdevops.xyz
export EDITOR='/usr/bin/nano'
#export K8S_VERSION=1.6.4
```

# After copying the above files to .bashrc run “ source .bashrc ”.

# Create a Cluster using Kops and generate a cluster file and save it carefully and do neccessary changes
``` bash
kops create cluster --name=pramothdevops.xyz \
--state=s3://pramothdevops.xyz --zones=us-east-1a,us-east-1b \
--node-count=2 --control-plane-count=1 --node-size=t3.medium --control-plane-size=t3.medium \
--control-plane-zones=us-east-1a --control-plane-volume-size 10 --node-volume-size 10 \
--ssh-public-key ~/.ssh/id_ed25519.pub \
--dns-zone=pramothdevops.xyz --dry-run --output yaml
```


# 6 Node cluster 

 kops create cluster --name=pramothdevops.xyz \
 --state=pramothdevops.xyz --zones=us-east-1a,us-east-1b,us-east-1c \
 --node-count=3 --master-count=3 --node-size=t3.medium --master-size=t3.medium \
 --master-zones=us-east-1a,us-east-1b,us-east-1c --master-volume-size 10 --node-volume-size 10 \
 --ssh-public-key ~/.ssh/id_rsa.pub \
 --dns-zone=pramothdevops.xyz --dry-run --output yaml


# One done run below commands to create the cluster 

``` bash

kops create -f cluster.yml
kops update cluster --name pramothdevops.xyz --yes --admin
kops validate cluster --wait 10m
kops delete -f cluster.yml  --yes
```


