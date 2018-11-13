# INTRO

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
* CodeStar / Start a project: choose template "Java Spring web application" (Filters: web app, Java, EC2)
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

# CodeBuild
* Open up, check build history


## EC2: check deployment
...

## Cloud9: modify the code and commit
...

## CodePipeline: check automated deployment process and the result
...

## Pipeline actions: check build and deploy steps with .yml files (buildspec.yml, template.yml, appspec.yml)

# AWS - Flovtec setup
...
