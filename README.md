<!DOCTYPE html>
<html lang="en">
<head>
<!--     <meta charset="UTF-8"> -->
<!--     <meta name="viewport" content="width=device-width, initial-scale=1.0"> -->
<!--     <title>Cloud Resume Project Overview</title> -->
<!--     <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
        }
        h1, h2, h3 {
            color: #333;
        }
        ul {
            list-style-type: disc;
            padding-left: 20px;
        }
        code {
            background-color: #f4f4f4;
            padding: 2px 5px;
            border-radius: 5px;
        }
        .update {
            font-weight: bold;
            color: #0066cc;
        }
    </style> -->
</head>
<body>

![image](https://github.com/user-attachments/assets/643e53d0-414c-4179-ae8c-b3243300cb95)


<h1>Cloud Resume Project Overview</h1>

<h2>Architecture Diagram</h2>
<p>This project comprises a series of challenges designed to enhance your AWS expertise and provide practical experience with AWS services. The primary objective is to build and deploy a static website that hosts your resume. Alongside this, you'll integrate the site with a database, create an API, and utilize automation for building, testing, and deploying both the code and infrastructure. The challenge also offers optional extensions for further skill development in specific areas.</p>
<p>My focus area for these extensions is DevOps, which aligns with my professional interests.</p>

<h2>Table of Contents</h2>
<ul>
    <li><strong>Cloud Resume Project Overview</strong></li>
    <li><strong>Table of Contents</strong></li>
    <li><strong>Benefits of the Challenge</strong></li>
    <li><strong>Project Phases</strong>
        <ul>
            <li>Start 1: Certification</li>
                        <li>Phase 1: AWS Solutions Architect Associate</li>
            <li>Part 1: Frontend Development
                <ul>
                    <li>1.1 HTML</li>
                    <li>1.2 CSS</li>
                    <li>1.3 JavaScript</li>
                    <li>1.4 Static Assets</li>
                    <li>1.5 CloudFront</li>
                </ul>
            </li>
            <li>Part 2: API Development
                <ul>
                    <li>2.1 Database</li>
                    <li>2.2 API</li>
                    <li>2.3 Python</li>
                </ul>
            </li>
            <li>Part 3: Integrating Frontend and Backend
                <ul>
                    <li>3.1 Dynamic Visitor Counter</li>
                </ul>
            </li>
            <li>Part 4: Automation & CI/CD
                <ul>
                    <li>4.1 Infrastructure as Code (IaC)</li>
                    <li>4.2 CI/CD Pipeline</li>
                    <li>4.3 Monitoring</li>
                </ul>
            </li>
        </ul>
    </li>
</ul>

<h2>Benefits of the Challenge</h2>
<p>Completing this challenge equips you with a wide range of skills, especially those within the AWS ecosystem, including:</p>
<ul>
    <li><strong>Software Development</strong>: Both frontend and backend perspectives.</li>
    <li><strong>Infrastructure as Code (IaC)</strong>: Leveraging CloudFormation, SAM, CDK.</li>
    <li><strong>Continuous Integration/Continuous Deployment (CI/CD)</strong>: Utilizing AWS CodeBuild, AWS CodeDeploy, and AWS CodePipeline.</li>
    <li><strong>Serverless Architecture</strong>: Implementing AWS Lambda, API Gateway, DynamoDB, and S3.</li>
    <li><strong>Security</strong>: Managing IAM, bucket policies, and API authentication/authorization.</li>
    <li><strong>Networking</strong>: Handling DNS, routing, and traffic within AWS services like Route 53 and VPCs.</li>
</ul>

<h2>Project Phases</h2>

<h3>The start: Certification</h3>
<p> I also earned the AWS Certified Solutions Architect – Associate certification. <span class="update">You can view my <a href="https://www.credly.com/badges/3ad53495-8108-4290-81f2-22548a0cfa7b/public_url" target="_blank">Credly badge here</a></span>.</p>
<p>



<h3>Part 1: Frontend Development</h3>
<p>This phase involves crafting the visual part of the resume using HTML, CSS, and JavaScript.</p>

<h4>1.1 HTML</h4>
<p>The resume is built with basic HTML. The focus is on functionality rather than design, utilizing grid and flexbox layouts for a simple two-column structure.</p>

<h4>1.2 CSS</h4>
<p>Basic styling is applied with CSS to give the resume a clean, document-like appearance.</p>

<h4>1.3 JavaScript</h4>
<p>JavaScript is used to implement a visitor counter. Initially, <code>localStorage</code> was used to store the count, which was later migrated to AWS DynamoDB.</p>

<h4>1.4 Static Assets</h4>
<p>The resume includes several SVG icons sourced under the iconmonstr license from iconmonstr.com.</p>

<h4>1.5 CloudFront</h4>
<p>The resume is served exclusively through a CloudFront distribution. The S3 bucket that hosts the static content has public access blocked, and only allows requests from the CloudFront OAC. HTTP requests are automatically redirected to HTTPS.</p>

<h3>Part 2: API Development</h3>
<p>This phase extends the visitor counter into a full-fledged API that stores and retrieves data from DynamoDB.</p>

<h4>2.1 Database</h4>
<p>The visitor count is stored in a DynamoDB table, where it is updated each time someone visits the site.</p>

<h4>2.2 API</h4>
<p>Instead of directly interacting with DynamoDB, the JavaScript code communicates with an API Gateway, which triggers a Lambda function to update the visitor count.</p>

<h4>2.3 Python</h4>
<p>The Lambda function, written in Python 3.9 (upgraded to 3.10 in May 2023), handles the business logic of updating and returning the visitor count. The Python code is tested using <code>pytest</code> and <code>moto</code>, with tests located in the <code>src/backend/tests/</code> directory.</p>

<h3>Part 3: Integrating Frontend and Backend</h3>
<p>This phase involves embedding the DynamoDB-stored visitor count into the JavaScript code to dynamically display the count on the page.</p>

<h4>3.1 Dynamic Visitor Counter</h4>
<p>The script responsible for fetching and updating the counter is located in <code>src/frontend/scripts/visitCounter.js</code>. It sends an HTTP POST request to the API Gateway to retrieve and update the counter each time the page is loaded.</p>

<h3>Part 4: Automation & CI/CD</h3>
<p>Automation is a key part of this phase, focusing on setting up Infrastructure as Code (IaC) and Continuous Integration/Continuous Deployment (CI/CD) processes.</p>

<h4>4.1 Infrastructure as Code (IaC)</h4>
<p>All AWS resources are provisioned using <code>Terragrunt</code>, which wraps Terraform configurations to reduce code duplication and facilitate deployment across multiple environments.</p>
<ul>
    <li><code>api_gateway-lambda/</code>: Contains resources for API Gateway and Lambda, which depend on each other.</li>
    <li><code>dynamodb/</code>: Defines the DynamoDB table.</li>
    <li><code>s3-cloudfront/</code>: Includes resources for S3 and CloudFront.</li>
    <li><code>cloudwatch/</code>: Sets up a CloudWatch alarm to monitor the Lambda function’s error rate</li>
</ul>

<h4>4.2 CI/CD Pipeline</h4>
<p>GitHub Actions automate the deployment process, with a dedicated pipeline defined in <code>.github/workflows/pipeline.yaml</code>.</p>
<p>The pipeline:</p>
<ul>
    <li>Runs tests for both frontend (Cypress) and backend (Pytest).</li>
    <li>Deploys infrastructure using <code>Terragrunt</code> after tests pass.</li>
    <li>Invalidates the CloudFront cache to ensure the latest version of the website is served.</li>
    <li>Synchronizes updated assets with the S3 bucket.</li>
</ul>

<h4>4.3 Monitoring</h4>
<p>CloudWatch Alarms monitor Lambda metrics, calculating the error percentage. If errors exceed 30% within a 5-minute window, the alarm triggers and sends an email notification to the admin via SNS.</p>

</body>
</html>
