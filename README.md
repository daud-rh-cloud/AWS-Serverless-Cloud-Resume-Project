# AWS Cloud Resume Challenge 

## Project Overvie
For this project I built a fully serverless website on AWS. The website is hosted on Amazon S3, delivered through CloudFront, secured with HTTPS using ACM, connected to a custom domain through Route 53, and includes a visitor counter built with API Gateway, Lambda, and DynamoDB.

<img width="1335" height="749" alt="image" src="https://github.com/user-attachments/assets/62ca1387-f91e-4143-b443-bef6e7109abc" />




---

# Step 1 – Website Creation & S3 Hosting

I created a personal portfolio website using HTML, CSS, and JavaScript. I used an LLM to help generate the initial frontend and later customized it myself. Placeholder sections were left for certificates and the API URL that would be added later.

I then created an S3 bucket, enabled Static Website Hosting, and uploaded all website files, including images and certificates. The bucket remained private because access would later be handled through CloudFront.

<img width="1590" height="594" alt="image" src="https://github.com/user-attachments/assets/59ca2b40-0eee-467c-8225-95f4e725bfb7" />

<img width="1132" height="664" alt="image" src="https://github.com/user-attachments/assets/39fb1492-d218-4f3f-bd65-dc0029567cf7" />



---

# Step 2 – CloudFront Distribution

I created a CloudFront distribution and configured the S3 bucket as the origin. To keep the bucket secure, I used Origin Access Control (OAC), which automatically created the required bucket policy.

This allowed CloudFront to access the website while preventing direct public access to S3.

<img width="1641" height="597" alt="image" src="https://github.com/user-attachments/assets/43f71d9a-eea3-40fa-9970-162c4989b89d" />
Orgin Access----
<img width="1446" height="746" alt="image" src="https://github.com/user-attachments/assets/dc650d6c-cb9c-4364-873c-b63752af3269" />
Update the Bucket policy 
<img width="1021" height="591" alt="image" src="https://github.com/user-attachments/assets/b949247c-048c-4f21-b219-6debaa1f99e3" />



 

---

# Step 3 – Domain & Route 53

I purchased the domain **myappone.se** through One.com and created a hosted zone in Route 53.

AWS generated four nameservers which I copied into One.com's DNS settings. After DNS propagation (approximately 24 hours), Route 53 became the authoritative DNS provider for the domain.

**Screenshot 5 – Route 53 Hosted Zone**

**Screenshot 6 – Nameserver Configuration**

---

# Step 4 – HTTPS with ACM

To secure the website, I requested a TLS certificate from AWS Certificate Manager (ACM).

ACM provided a DNS validation record which I added to Route 53. Once validated, I attached the certificate to CloudFront and created Route 53 alias records pointing the domain to the CloudFront distribution.

Request flow:

```text
User → myappone.se → Route 53 → CloudFront → S3
```

**Screenshot 7 – ACM Certificate**

**Screenshot 8 – Route 53 Alias Record**

---

# Step 5 – Visitor Counter Backend

I created a DynamoDB table to store the visitor count and a Python Lambda function that increments the counter every time the website is loaded.

The Lambda function was connected to API Gateway using an HTTP API. The generated API URL was added to the website's JavaScript code so the counter updates automatically whenever a user visits the page.

Request flow:

```text
Browser → API Gateway → Lambda → DynamoDB → Browser
```

**Screenshot 9 – DynamoDB Table**

**Screenshot 10 – Lambda Function**

**Screenshot 11 – API Gateway**

**Screenshot 12 – Visitor Counter Working**

---

# What I Learned

* Static website hosting with S3
* CloudFront and Origin Access Control (OAC)
* DNS and Route 53
* TLS certificates using ACM
* Serverless applications with Lambda
* API creation using API Gateway
* Data storage with DynamoDB
* IAM roles and least privilege access
