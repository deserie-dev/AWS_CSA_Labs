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

</p></details>

<details>
<summary><b>ELB, CloudWatch & Auto Scaling</b></summary><p>

</p></details>

<details>
<summary><b>IAM</b></summary><p>

</p></details>

<details>
<summary><b>Databases</b></summary><p>

</p></details>

<details>
<summary><b>SQS, SWF & SNS</b></summary><p>

</p></details>

<details>
<summary><b>DNS & Route 53</b></summary><p>

</p></details>

<details>
<summary><b>ElastiCache</b></summary><p>

</p></details>

<details>
<summary><b>Security</b></summary><p>

</p></details>

<details>
<summary><b>Architecture Best Practices</b></summary><p>

</p></details>
