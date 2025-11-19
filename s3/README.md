# Part 1: Hosting A Static Website on Amazon S3 With A Custom Domain Name

**prerequisite:**
* Create your own public domain name via a domain name provider (ex: GoDaddy.com)
* Create a Route53 Public Hosted Zone for same domain and update Route53 nameservers into your domain registrar DNS settings.

## Steps
1. Create an S3 bucket for your website (make sure that the bucket is public by unchecking the "Block all public access" box during setup). 
![alt text](photos/bucket1.png)
![alt text](photos/bucket2.png)
2. Upload static website content to your bucket
![alt text](photos/bucket3.png)
3. Enable your S3 bucket for website hosting with an index document (index.html)
![alt text](photos/bucket4.png)
![alt text](photos/bucket5.png)
4. Modify bucket permissions to allow public access. Unblock "Block all public access" settings and add bucket policy.
![alt text](photos/bucket6.png)
![alt text](photos/bucket7.png)
5. Access the bucket using the bucket website endpoint
![alt text](photos/bucket8.png)
![alt text](photos/bucket9.png)
6. In your Route53 public hosted zone, create an alias record for your domain name pointing to the S3 bucket endpoint (this way you don't have to use the endpoint name but can use your domain name instead which is usually shorter/easier to remember)
![alt text](photos/bucket10.png)
![alt text](photos/bucket11.png)

# Part 2: Securing Your S3 Static Website with HTTPS and CloudFront

## Steps
1. Create a TLS certificate for your domain name by using Amazon Certificate Manager (it must be created in the N. Virginia region!)
![alt text](photos/acm1.png)
- click on your certificate ID, and in the Domains section select "Create records in Route 53"
![alt text](photos/acm2.png)
![alt text](photos/acm3.png)
2. Create a CloudFront distribution with the website endpoint as the origin. Confiugre the viewer protocol policy to redirect HTTP to HTTPS
![alt text](photos/cdfn1.png)
- During the setup ensure you set viewer protocol policy to "Redirect HTTP to HTTPS" (this ensures no one can access the website over HTTP only HTTPS, making it more secure)
![alt text](photos/cdfn2.png)
- Additionally in the setup ensure the Custom SSL certificate is set to use the one you generated via Amazon Certificate Manager
![alt text](photos/cdfn3.png)
- the rest of the cloudfront settings can be left as default
3. Update your Route53 record to point to the CloudFront distribution
- Select your record, and in the edit record box, under "Route traffic to" select Alias to CloudFront distribution, and choose your distribution from the dropdown
![alt text](photos/cdfn4.png)
4. Try accessing your website via the domain name, it should now be secured via https (ex: https://www.domainname.com)
![alt text](photos/cdfn5.png)
![alt text](photos/cdfn6.png)