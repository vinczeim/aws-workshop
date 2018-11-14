# INTRO

[Imre Vincze](https://www.linkedin.com/in/vinnie950) - head of IT @ [flov technologies AG](https://www.linkedin.com/company/flov-technologies) (Flovtec)

## Flovtec
* https://www.flovtec.com
* Vision: asset manager company providing liquidity for digital assets
* Step 1: 
  * assets: crytpo-currencies
  * market making: on crypto exchanges
* Long term:
  * assets: any kind of digital assets, anything that got tokenized
  * market making: not on exchanges but decentralized, peer-to-peer
* Team: asset managers + quantitative researchers + developers
* We are HIRING !!!

## Infra
* Startup with NO infrastructure -> building everything from scratch
* Setting up infra in Amazon cloud
* Trying to keep it protected by AWS access control (regulators "like it")
* Usual first requirements: dev workspaces, code repo, database, automated CI/CD, segregation of DEV/UAT/PROD execution environments

## Plan for today
* Create account with billing alarm, create users/groups, create CI/CD pipeline for a Java web application
* Show current Flovtec setup


# AWS - CodeStar / CodePipeline setup

## Create a new AWS account
* AWS Console: https://aws.amazon.com
* Account creation guide: https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account
* My account: flovtrain
* Only one account is allowed per e-mail address: created aliases (aws1@flovtec.com *, aws2@flovtec.com, aws3@flovtec.com)

## Regions and available services
* Regions and availability zones (data centers)
* Region table: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/

## IAM: create users and groups with policies
* IAM = Identity & Access Management: Users, Groups, Roles and Policies
* IAM is Global
* Root account: logs in with sign-up e-mail address
* Initial steps:
  * Customize users sign-in link
  * Activate MFA on root account
  * Create users: imre, john -> Create group: system-admins with policy AdministratorAccess -> Download access key .csv
  * Set password policy
* Access methods and credentials:
  * User + password: to access AWS Console (via browser)
  * Access key ID + Secret access key: to access AWS programmatically (e.g. AWS CLI or Eclipse plugin)
  * Git credentials: to access CodeCommit repo by Git client
  * Check user's Security Credentials to manage

## Create billing alert
* Do as root
* My Billing Dashboard / scroll down to Alerts & Notifications / Enable Now
  * Check Receive Billing Alerts
  * Save preferences
  * Click Manage Billing Alerts -> CloudWatch / Billing / Create Alarm / set amount and e-mail address / Confirm e-mail address

## CodeStar: create new project (Java web app running on EC2)
* Log on with the admin user that we just created
* Select region: Ireland (to be able to use Cloud9)
* CodeStar / Start a project:
  * Choose template "Java Spring web application" (Filters: web app, Java, EC2)
  * EC2 configuration: leave on default (t2.micro instance with default VPC)
  * Add permission to administer AWS resources on your behalf
  * Choose an Amazon EC2 Key Pair (needed to SSH to EC2) -> Create new (in EC2 service / Key Pairs) then save private key
  * Select key pair and press Create
  * Choose Cloud9 as IDE, leave its settings on default, note that it shuts down in 30 minutes
* Check the CodeStar project's dashboard, note that the pipeline is already building

## CodeCommit
* Open from CodeStar's left side menu, pipeline stage or as individual service
* Check the project files and their descriptions in README.md
* Features: clone URL, history, compare, branches, tags, pull requests

## CodeBuild
* Open and check build history
* Download/view the build artifact
* Uses buildspec.yml

## CodeDeploy
* Open and check deployment history
* Check deployment groups and revisions (stored in S3 bucket)
* Uses appspec.yml

## CodePipeline
* It wires the previous steps together
* Ability to release change or retry failed step (only if the pipeline itself didn't change)
* Press Edit and then Edit for each stage and each action to review settings

## CloudFormation
* Infrastructure as Code (IaC)
* Used template.yml

## CodeStar again
* What does it add on top of CodePipeline?
  * Users for this dev workflow, with ability to use or even edit the pipeline
  * Central dashboard
* Check Project Resources to see how many things are created in the background

## Basic building blocks: EC2 and S3
* S3: storage space
* EC2: virtual box

## EC2: check deployment
* Open EC2 service and check our instances: one was created for the web app and another for Cloud9
* SSH to the web app box and check deployment (private key .pem file is needed)
* Get pulic IP from EC2 service and view the web app in a browser

## Cloud9: modify the code and commit
* Start Cloud9 and let it check out our code
* Set a dark theme to be cool !!!
* Set Git commit info:
  * git config --global user.name YOUR_USER_NAME
  * git config --global user.email YOUR_EMAIL_ADDRESS
* Change the file /mycloud9webapp/src/main/webapp/WEB-INF/views/index.jsp and commit the change
  * cd mycloud9webapp
  * git commit -a
  * git push

## CodePipeline: check automated deployment process and the result
* Check the result in CodeCommit and see CodePipeline building
* Check how the web site changed


# AWS - Flovtec setup

## How is our setup different?
* Dedicated DEV/UAT/PROD EC2 instances (actually deployment groups)
* Only DEV is deployed on every commit, UAT and PROD require manual approval
* DEV/UAT is managed by one admin user and PROD is managed by another admin user
* Connection between DEV/UAT and PROD will be a shared S3 bucket (staging area) owned by the PROD account
* DEV and UAT located in Ireland, PROD in N. Virginia (to be close to the exchange)
* Additional steps for CodeBuild: test execution, static code analysis

## What else do we use?
* S3: store (and even receive) exchange market data in .csv files
* RDS: MySQL DB
* Route 53: route requests from our registered domain to the load balancers
* EC2 / Load Balancers: map port 80 requests to port 8090, distribute load (coming soon), make provision of new EC2 instances transparent (IP address changes but we refer to instance ID which remains the same)
* Workspaces: Amazon Linux 2 instances because Cloud9 is not good enough (yet) for Java development

## What is still coming?
* Athena: use .csv data in S3 as DB (run SQL queries) without loading into a DB
* SQS / SNS: Queue and topic based messaging middleware
* Kinesis Data Firehose: streaming alternative for messaging and even much more to hook analytics into the stream
* Glacier: low-cost data backup
* CloudWatch: runtime monitoring
* Systems Manager: Operational data
...


# References
* [AWS Docs](https://docs.aws.amazon.com)
* [AWS Whitepapers](https://aws.amazon.com/whitepapers)
  * [Overview of all AWS services](https://docs.aws.amazon.com/aws-technical-content/latest/aws-overview/introduction.html)
  * [Blue/Green Deployments on AWS](https://d1.awsstatic.com/whitepapers/AWS_Blue_Green_Deployments.pdf)
  * [Continuous Integration and Continuous Delivery on AWS](https://d1.awsstatic.com/whitepapers/DevOps/practicing-continuous-integration-continuous-delivery-on-AWS.pdf)
