# Part 1: Create VPC Peering between VPCs across AWS regions and connect to EC2 instance over private IP by using A VPC peering connection

## Architecture 
![alt text](photos-1/architecture.png)

## Steps
1. Create 2 VPCs in different AWS regions, create an internet gateway and associate it with VPC-A, VPC-B does not need an internet gateway.
2. Create public and private subnets in the respective VPCs (VPC-A & VPC-B)
3. Launch EC2 instances in respective subnets. Only the EC2 instance in the public subnet of VPC-A should have a public IP. Create security groups to allow SSH from EC2-A to EC2-B and test the connection by using SSH and ping from EC2-B to EC2-C
![alt text](photos-1/instances1.png)
4. Login to EC2-A and connect via SSH to EC2-B. Try to ping EC2-C, you should not be able to reach EC2-C via EC2-B.
![alt text](photos-1/instances2.png)
5. Create VPC peering between both the VPCs
![alt text](photos-1/peering1.png)
![alt text](photos-1/peering2.png)
    - Make sure after you establish the intial VPC peering connection to go to the region that VPC-B is in, and accept the peering connection from there
    ![alt text](photos-1/peering3.png)
6. Modify both VPC private subnet route tables and add routes for the destination VPC with VPC peering as the target (just creating the peering connection isn't enough for the resources in both environments to communicate with one another)
    - In the route table for VPC-B we show that if the traffic is coming from VPC-A (desination: 10.100.0.0/16) the target should be the VPC peering connection we created.
    ![alt text](photos-1/peering4.png)
    ![alt text](photos-1/peering5.png)
- Do the same for the route table in VPC-A
![alt text](photos-1/peering6.png)
7. Now if you trying pinging EC2-C via EC2-B you should get a response
![alt text](photos-1/peering7.png)

# Part 2: Create a VPC endpoint gateway for S3 and access S3 contents from an EC2 instance in a Private subnet without requiring an internet connection

## Architecture
![alt text](photos-2/architecture.png)

## Steps
1. Create a VPC, internet gateway, public subnet and private subnet
2. Launch an EC2 instance in each of the subnets. Only EC2-A should have a public IP. Ensure that your security groups allow for SSH from EC2-A to EC2-B.
3. Create a S3 bucket in the same region and upload a random sample file
![alt text](photos-2/bucket1.png)
![alt text](photos-2/bucket2.png)
4. Create an IAM role for the EC2 instance and attach the S3 read-only IAM policy. Associate the role with EC2-B.
![alt text](photos-2/iam1.png)
![alt text](photos-2/iam2.png)
- After creating the role, modify the IAM role of EC2-B to use your newly created one.
![alt text](photos-2/instance1.png)
![alt text](photos-2/instance2.png)
5. Login to EC2-B and try to download the sample file stored in your S3 bucket via the AWS CLI. It should not work.
![alt text](photos-2/instance3.png)
6. Create a VPC endpoint (type: gateway) for S3 and update the Private subnet route table.
![alt text](photos-2/endpoint1.png)
![alt text](photos-2/endpoint2.png)
7. Try to download the same file from S3 again. It should now work.
![alt text](photos-2/instance4.png)

# Part 3: Create and use VPC Private Link to expose your Web service privately to application hosted in another VPC

## Steps

# Part 4: Advanced Networking: Setup Site-To-Site VPN between AWS VPC and simulated on-premise network

## Steps

# Part 5: Advanced Networking: Setup Site-To-Site VPN between AWS VPC and simulated on-premise network

## Steps