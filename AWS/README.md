# AWS

## ECR

Login with docker

```
aws ecr get-login-password --region <REGION> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<REGION>.amazonaws.com
```

# References

- https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-cli.html

## AMI 

### Start userdata scripts always

```
Content-Type: multipart/mixed; boundary="//"
MIME-Version: 1.0

--//
Content-Type: text/cloud-config; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="cloud-config.txt"

#cloud-config
cloud_final_modules:
- [scripts-user, always]

--//
Content-Type: text/x-shellscript; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="userdata.txt"

#!/bin/bash
printf "\n*** $(date +'%Y-%m-%d %H:%M:%S') SETUP ON DEPLOYMENT INSTANCE STARTING\n"

sudo dd if=/dev/nvme0n1 of=/dev/null bs=5M

printf "\n*** $(date +'%Y-%m-%d %H:%M:%S') SETUP ON DEPLOYMENT INSTANCE FISNISHED\n"
--//
```