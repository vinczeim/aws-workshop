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
Access methods and credentials:
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
...

## CodeCommit
...

## EC2: check deployment
...

## Cloud9: modify the code and commit
...

## CodePipeline: check automated deployment process and the result
...

## Pipeline actions: check build and deploy steps with .yml files (buildspec.yml, template.yml, appspec.yml)

# AWS - Flovtec setup
...
