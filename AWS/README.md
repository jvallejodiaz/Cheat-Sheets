# AWS

## ECR

Login with docker

```
aws ecr get-login-password --region <REGION> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<REGION>.amazonaws.com
```

# References

- https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-cli.html