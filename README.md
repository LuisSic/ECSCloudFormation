# ECSCloudFormation

This example show how to create a ECS cluster whit EC2 instances and application load balancer.

## Getting Started

Next, the parameters of each yaml file will be explained.

## VPC.yml

This yml file creates a VPC with diferents resources ( 3 Public Subnets, 3 Private Subnets, DMZ Security Group, Nat Gateway and Internet Gateway).

### Parameters

* EnvironmentName: An environment name that is prefixed to resource names
* VpcCIDR: The IP range (CIDR notation) for this VPC
* PublicSubnet1CIDR: The IP range (CIDR notation) for the public subnet in the first Availability Zone
* PublicSubnet2CIDR: The IP range (CIDR notation) for the public subnet in the second Availability Zone
* PublicSubnet3CIDR: The IP range (CIDR notation) for the public subnet in the third Availability Zone
* PrivateSubnet1CIDR: The IP range (CIDR notation) for the private subnet in the first Availability Zone
* PrivateSubnet2CIDR: The IP range (CIDR notation) for the private subnet in the second Availability Zone
* PrivateSubnet3CIDR: The IP range (CIDR notation) for the private subnet in the third Availability Zone

## cluster.yml

This yaml file creates a cluster and automatically registers our ec2s in the cluster.

### Parameters

* Ami: Amazon ECS-optimized AMI
* EC2InstanceType: Instance type for ec2
* EC2SecurityGroup: Security Group to use for the ECS cluster hosts (Obtained from the outputs of the vpc yaml file)
* ClusterSize: How many ECS hosts do you want to initially deploy?
* ListSubnets: subnets where this ECS cluster should be deployed (Obtained from the outputs of the vpc yaml file)
* EnvironmentName: An environment name that is prefixed to resource names

## lb.yml
This template deploys an Application Load Balancer that exposes our various ECS services.

### Parameters

* EnvironmentName: An environment name that is prefixed to resource names
* SecurityGroup: Security Group for application load balancer (Obtained from the outputs of the vpc yaml file)
* ListSubnets:  subnets for deploy application load balancer (Obtained from the outputs of the vpc yaml file)
* VPC: Vpc for deploy application load balancer (Obtained from the outputs of the vpc yaml file)

## service.yml

This is an example of an ECS service that displays a static web page.

### Parameters

* EnvironmentName: An environment name that is prefixed to resource names
* Cluster: Cluster where the service will be deployed (Obtained from the outputs of the cluster yaml file)
* AppName:  Container name
* AppContainerPort: The port number on the container
* AppHostPort: Port for de docker host
* IdImage: The image used to start a container
* ECSDesiredCount:  Number of tasks that will run in the cluster
* TargetGroup: Target group to associate service and tasks with load balancer (Obtained from the outputs of the lb yaml file)

## main.yml
This file is used to create a nested stack, for templates that are separated. This file is the one in charge of deploy the entire infrastructure

## Infrastructure

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds


## Authors

* **Luis Sic** - *TT* - [sluis117](https://github.com/LuisSic)


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
