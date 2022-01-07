# AWS Certified Solutions Architect Labs

---

<details>
<summary><b>S3</b></summary><p>

1. Create an Amazon Simple Storage Service (Amazon S3).

![](/images/create-bucket.png)

2. Upload, Make Public, Rename, and Delete Objects in Your Bucket.

![](/images/upload.png)

![](/images/make-public.png)

![](/images/delete-object.png)

3. Enable Version Control

3.1 Enable Versioning

![](/images/versioning-1.png)

3.2 Create Multiple Versions of an Object

![](/images/versions.png)

4. Enable Static Hosting on Your Bucket

![](/images/static-website-2.png)

![](/images/static-website.png)

</p></details>

<details>
<summary><b>EC2</b></summary><p>

## Launch and Connect to a Linux Instance

In this exercise, I launched a Linux instance and connected to it through SSH.

The instance has the following configuration:

- AMI: Ubuntu 18
- Instance Type: t2-micro
- Network: default
- Subnet: No preference
- Auto-assign Public IP: Enable
- user data box:

```
#!/bin/bash
yum update -y
yum install -y httpd
yum install -y wget
chkconfig httpd on
cd /var/www/html
service httpd start
```

- Add Tags:

Key: Name
Value: Webserver

- Security group with the following values:

Security group name: CSALab
Description: CSALab

- Add Rule, and set the following values (leave the default SSH rule):

Type: HTTP
Source: My IP

---

![](/images/ec2-1.png)

![](/images/ec2-ssh.png)

---

## Launch a Spot Instance

In this exercise, I created a Spot Instance.

![](/images/spot.png)

---

## Create an Amazon EBS Volume and Show That It Remains After the Instance Is Terminated

In this exercise, I demonstrated how an Amazon EBS volume persists beyond the life of an
instance.

I created an EC2 instance and added a second Amazon EBS volume of size 50 GB.

After terminating the instance, the boot drive is destroyed, but the additional Amazon EBS volume remains and now says Available.

![](/images/ebs-1.png)

---

## Take a Snapshot and Restore

![](/images/snapshot.png)

![](/images/restore-volume-1.png)

![](/images/restore-volume-2.png)

</p></details>

<details>
<summary><b>VPC</b></summary><p>

# Create a Custom Amazon VPC

![](/images/create-vpc.png)

# Create Two Subnets for Your Custom Amazon VPC

1. Create a subnet with a CIDR block equal to 192.168.1.0/24. Create the subnet in the Amazon VPC from above exercise 4.1, and specify an Availability Zone for the subnet (for example, US-East-1a).

2. Create a subnet with a CIDR block equal to 192.168.2.0/24. Create the subnet in the Amazon VPC from above exercise 4.1, and specify a different Availability Zone for the subnet than previously specified (for example, US-East-1b).

![](/images/create-subnets.png)

---

# Connect Your Custom Amazon VPC to the Internet and Establish Routing

1. Create an internet gateway and attach it to your custom Amazon VPC.

![](/images/create-igw.png)

2. Add a route to the main route table for your custom Amazon VPC that directs Internet traffic (0.0.0.0/0) to the IGW.

![](/images/update-route-table.png)

3. Create a NAT gateway, place it in the public subnet of your custom Amazon VPC, and assign it an EIP.

![](/images/create-nat.png)

4. Create a new route table and place it within your custom Amazon VPC. Add a route to it that directs Internet traffic (0.0.0.0/0) to the NAT gateway and associate it with the private subnet.

![](/images/create-route-table.png)

You have now created a connection to the Internet for resources within your Amazon VPC. You established routing rules that direct Internet traffic to the IGW regardless of the originating subnet.

</p></details>

<details>
<summary><b>ELB, CloudWatch & Auto Scaling</b></summary><p>

# Application Load Balancer Lab

1. Setup base infrastructure:

- VPC

![](/images/vpc.png)

- create 4 subnets in the above VPC, 2 public(for the elb), 2 private(for the ec2 instances)

![](/images/subnets.png)

- create an internet gateway for internet access for public subnets

![](/images/igw.png)

- attach igw to the vpc

![](/images/attach-igw.png)

- create a NAT gateway in a public subnet(this will provide internet access to VM's in the private subnets)

![](/images/nat.png)

- add routes to the route table of the above vpc to allow internet connectivity (remember, every VPC has a default route table)

![](/images/route1.png)

- associate public subnets to this route table

![](/images/ass-pub-sub.png)

- create route table for NAT gateway

![](/images/nat-route.png)

- edit routes for above route table to allow internet traffic

![](/images/route2.png)

- associate private subnets to this route table

![](/images/ass-priv-sub.png)

Now that have created the base infra, create the EC2 instances

- create 2 EC2 instances, one in each private subnet . In user data add bash script to install web server

```
#!/bin/bash
yum install httpd -y
systemctl enable httpd
echo '<h1>This is instance1"</h1>' > /var/www/html/index.html
systemctl start httpd
```

![](/images/ec2.png)

- create an application load balancer

![](/images/elb.png)

- create a target group with the 2 instances

![](/images/target.png)

- edit the security group for the instances. Edit inbound rules to allow the load balancer to send traffic to the instances

![](/images/edit-sg.png)

- Go back to target group dashboard to confirm the health status of the EC2 instances

![](/images/health.png)

---

# Launch Configuration & Scaling Group

AWS now recommends using a launch template instead of a lauch configuration, so I created a launch templete and used it to create an auto-scaling group.

![](/images/lt.png)

![](/images/asg.png)

</p></details>

<details>
<summary><b>IAM</b></summary><p>

# Create an IAM Group

In this exercise, I create a group for all IAM administrator users and assign the proper permissions to the new group.

1. Log in as the root user.
2. Create an IAM group called Administrators.
3. Attach the managed policy, IAMFullAccess, to the Administrators group.

![](/images/group.png)

---

# Create an IAM User

Here I create an IAM user who can perform all administrative IAM functions.

1. While logged in as the root user, create a new IAM user called Administrator.
2. Add your new user to the Administrators group.
3. On the Details page for the administrator user, create a password.

![](/images/user.png)

</p></details>

<details>
<summary><b>Databases</b></summary><p>

# Create a MySQL Amazon RDS Instance

![](/images/rds.png)

---

# Create a Read Replica

![](/images/replica.png)

---

# Read and Write from a DynamoDB Table

1. Create a new table named UserProfile with a partition key of userID of type String

![](/images/dynamodb.png)

2. Using the Amazon DynamoDB console, create and save a new item in the table. Set the userID to U01, and append another String attribute called name with a value of Deserie.

![](/images/dd1.png)

![](/images/dd2.png)

---

</p></details>

<details>
<summary><b>SQS, SWF & SNS</b></summary><p>

# Create an Amazon SNS Topic

![](/images/topic1.png)

---

# Create a Subscription to Your Topic

![](/images/topic2.png)

![](/images/topic3.png)

---

# Publish to a Topic

![](/images/publish1.png)

![](/images/publish2.png)

---

# Create Queue

1. Create a new queue with input as the queue name, 60 seconds for the default visibility, and 5 minutes for the message retention period. Leave the remaining default values for this exercise.

![](/images/sqs1.png)

</p></details>

<details>
<summary><b>DNS & Route 53</b></summary><p>

</p></details>

<details>
<summary><b>ElastiCache</b></summary><p>

# Create an Amazon ElastiCache Cluster Running Memcached

![](/images/memcached1.png)

# Create an Amazon ElastiCache Cluster Running Redis

![](/images/memcached1.png)

</p></details>

<details>
<summary><b>Security</b></summary><p>

</p></details>

<details>
<summary><b>Architecture Best Practices</b></summary><p>

</p></details>
