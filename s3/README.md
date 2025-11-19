# Hosting A Static Website on Amazon S3 With A Custom Domain Name

**prerequisite:**
* Create your own public domain name via a domain name provider (ex: GoDaddy.com)
* Create a Route53 Public Hosted Zone for same domain and update Route53 nameservers into your domain registrar DNS settings.

## Steps
1. Create an S3 bucket for your website. 
2. Upload static website content to your bucket
3. Enable your S3 bucket for website hosting with an index document (index.html)
4. Modify bucket permissions to allow public access. Unblock "Block all public access" settings and add bucket policy.
5. Access the bucket using http://bucket-name.s3-website-region.amazonaws.com
6. In Route53 public hosted zone, create an alias record for your www domain name pointing to S3 bucket endpoint. Access the website using http://www.domain-name
7. Optional step: Con