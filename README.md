# Udagram - Cloudformation Script

This repository is created for Udagram Applicaiton.

I created 2 scripts for creating infrastructure and required servers for application in order to avoid a long script.

## Step-1: Creating key files

As first and foremost, I created 2 key files from AWS Console.

- `jumpbox-key.pem` for bastion host/jumpbox
- `private-devops-key.pem` for private servers

![/screenshots/key-files.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/key-files.png)


## Step-2: Creating Infrastructure

Use this script [udagram-infra.yml](https://github.com/Marn111/udagram-cloudformation-script/blob/main/udagram-infra.yml) to create required VPCs, Subnets, Internet Gateway, Routing tables, etc..


### Usage

```bash
cd udagram-cloudformation-script
create.sh udagraminfra udagram-infra.yml udagram-infra-params.json
```

### Outputs

![/screenshots/udagraminfra-outputs.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/udagraminfra-outputs.png)

## Step-3: Deploying servers with required security groups

Use this script [udagram-server.yml](https://github.com/Marn111/udagram-cloudformation-script/blob/main/udagram-server.yml) to create as following - 

- Load Balancer
- Security Groups
- Deploying instances by load balancer using LaunchConfiguration
- Creating AMI Role to access S3 bucket
- Creating Instance profile and attach to instances
- Creating Bastion host to access to private servers
- etc..

### Usage

```bash
create.sh udagram udagram-server.yml udagram-server-params.json
```

### Outputs

**Udagram** application is deployed as following screenshot.

In the outputs, you will see **LoadBalancerDNS** is concatenated with `http://`.

> [http://udagr-WebAp-10KNR64ZJYD7V-250719208.us-east-1.elb.amazonaws.com](http://udagr-WebAp-10KNR64ZJYD7V-250719208.us-east-1.elb.amazonaws.com)

![/screenshots/udagram-outputs.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/udagram-outputs.png)

**Load Balancer Screenshot**

![/screenshots/LoadBalancer.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/LoadBalancer.png)

**Browsing DNS**

![/screenshots/browsing-DNS.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/browsing-DNS.png)


## Addition for Development purpose:
**Jumpbox** is created with specific Security Group which allow to my home IP address. 

> PS: In this case, I assumed we created development servers(EC2 Instances) with `private-devops-key.pem`. After testing all of following flows, I updated to Launch Configuration by removing `keyName: private-devops-key` from `udagram-server.yml` script, in order to prevent ssh to production servers.

### Usage

```bash
create.sh jumpbox jumpbox.yml jumpbox-params.json
```

### Outputs

![/screenshots/jumpbox-outputs.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/jumpbox-outputs.png)


### Use cases
1. Jumpbox is accessed via my home IP address

![/screenshots/Access-to-jumpbox.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/Access-to-jumpbox.png)

2. Copy `private-devops-key.pem` into jumpbox

![/screenshots/copy-privatekey-into-jumpbox.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/copy-privatekey-into-jumpbox.png)

3. Accessing to PrivateInstance1 from jumpbox(10.0.2.75)

> Picture: PrivateInstance1
![/screenshots/PrivateInstance1.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/PrivateInstance1.png)

> Picture: Accessing from jumpbox
![/screenshots/jumpbox-access-private-server1.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/jumpbox-access-private-server1.png)

4. Accessing to PrivateInstance2 from jumpbox(10.0.2.80)

> Picture: PrivateInstance2
![/screenshots/PrivateInstance2.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/PrivateInstance2.png)

> Picture: Accessing from jumpbox
![/screenshots/jumpbox-access-private-server2.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/jumpbox-access-private-server2.png)

5. Accessing to PrivateInstance3 from jumpbox(10.0.3.54)

> Picture: PrivateInstance3
![/screenshots/PrivateInstance3.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/PrivateInstance3.png)

> Picture: Accessing from jumpbox
![/screenshots/jumpbox-access-private-server3.png](https://github.com/Marn111/udagram-cloudformation-script/blob/main/screenshots/jumpbox-access-private-server3.png)



Authored by: Marn111/2022
