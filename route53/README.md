# Route53 DNS Region Level Failover

## Steps
1. Launch an ec2 instance and assign a public IP to it. Allow SSH and HTTP in its security group.
2. Install a httpd web server on the instance
![alt text](photos/httpd.png)
![alt text](photos/httpd1.png)
3. Create an elastic IP and assign it to the EC2 instance
![alt text](photos/eip.png)
4. Validate that you can access the web page over the internet using the EC2's elastic IP
![alt text](photos/eip1.png)