# AWS EC2 Tutorial

1. Go to

[AWS EC2](https://console.aws.amazon.com/ec2/)

2. Create an EC2 instance

* Click **Launch Instance**
* Click **Amazon Linux**
* Click **Create new key pair**

3. PEM keys

Give a name on **Key pair name** and leave **RSA** and **.pem** type
Download your PEM key e.g. **4May23.pem**

4. Launch instance by clicking **Launch instance**

5. See your instance by clicking **View all instances**

6. Change user permissons to PEM keys

```bash
chmod 400 4May23.pem
```
7. Connect the EC2 via ssh whereas user is as e.g. **ec2-user** and host is the **Public IPv4 DNS** point, e.g., ec2-<>.compute-1.amazonaws.com

```bash
ssh -i <cert.pem> <user>@<host>
```
