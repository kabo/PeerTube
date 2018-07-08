# Running PeerTube on AWS

This is a work in progress.

I'm thinking it can be done in the "traditional" way, or the docker way.

Traditional plan:

 - [ ] Cloudformation stack to set up VPC
 - [ ] Cloudformation stack to set up an EC2 instance, security group, etc.
 - [ ] Cloudformation stack to set up an EC2 instance and install PeerTube
 - [ ] Scripts to set up ElasticBeanstalk with PeerTube
 - [ ] Cloudformation stack to set up Postgresql RDS
 - [ ] Scripts to set up ElasticBeanstalk with autoscaling PeerTube using RDS

Docker plan:

 - [x] Cloudformation stack to set up VPC
 - [ ] Cloudformation stack to set up security group, RDS, ElastiCache, etc.
 - [ ] Scripts to set up EKS with the PeerTube docker image
 - [ ] Cloudformation stack to set up CloudFront distribution

After that I have ideas, but I'm not yet sure what's the right way forward.

 - Redis: ElastiCache or make it work over SQS also
 - What is redis used for? Should there be a worker pool pulling stuff of a work queue? Can it be done by lamdas?
 - Run the PeerTube docker container in AWS EKS, video encoding workers in Fargate?

## Set up

### Cloudformation VPC

This stack has infrastructure stuff

```shell
aws cloudformation create-stack --stack-name peertube-vpc --template-body file://./cloudformation-vpc.yml
```

### Cloudformation state holders

This stack has the stuff that holds state, such as databases

```shell
aws cloudformation create-stack --stack-name peertube-state --template-body file://./cloudformation-state.yml
```


