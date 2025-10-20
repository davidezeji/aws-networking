# aws-networking
Projects demonstrating secure, highly available AWS networking architectures, integrating private connectivity, inter-VPC communication, and scalable routing solutions to support enterprise workloads and multi-account environments.

## Tech Stack

**EC2**
* Create and use NAT EC2 instance instead of NAT Gateway

**VPC**
* Create VPC Peering between VPCs across AWS regions and connect to EC2 instance over private IP by using VPC peering connection

* Create VPC endpoint gateway for S3 and access S3 contents from EC2 instance in Private subnet without requiring internet connection

* Create and use VPC Private Link to expose your Web service privately to application hosted in another VPC

* Advanced Networking: Setup Site-To-Site VPN between AWS VPC and simulated on-premise network

* Transit Gateway - Setup communication between multiple VPCs

**Route53**
* Implement AWS region level failover using AWS Route53

**S3**
* Hosting website on S3 using custom domain name from GoDaddy

* Hosting HTTPS enabled website using S3 and CloudFront

**VPN**
* AWS Client VPN and various scenarios like accessing Internet, Split Tunnel, accessing Peered VPCs via Client VPN connection