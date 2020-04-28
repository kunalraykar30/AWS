# AWS
#### Author: Kunal Raykar
Objective is to create the VPC, Subnet, IGW, EC2 with Ansible in one go...
All componenets are coded in yaml so you can run the code from Bastion host and build your Infra in one shot.

create_ec2.yml

While running the playbook make sure that the ~/var directory is present.
All the variables are passed in the var_alldetails which contain name of the VPC,subnet,IGW,Elastic IP etc.
The values mentioned in the var_alldetails will be used by yaml file to set up the Infra components.

/var
-var_alldetails

Command to be executed:
```
[root@Bastion_host]# ansible-playbook create_ec2.yml
```
Here aws-region=eu-central-1 is mentioned and all Infra components will be created in this region. 

Here, I have created a VPC with two Availability Zones [AZ-1 and AZ-2]. As AWS Availability Zones are physically separated, and their power supply are different, so that in the case of a power outage, not all zones are impacted. In VPC 4 subnets (2 public, 2 privates) are drawn. Also, 2 Elastic IPs and 2 NAT Gateways (one per AZ) are created. 
We double the NAT Gateways so that each AZ can be completely independent.

##### NOTE: I generally have used Bastion host to perform the tasks. Make sure that git,ansible,boto3,boto,python are installed on Bastion host. Also, You need to create one role and assign to your bastion host in order for your bastion host to spun up Infra components. I have not used any AWS credentials here because I am using AWS bastion host to create all the Infra components. 
