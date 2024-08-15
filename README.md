### Project Overview:

This project sets up a Continuous Integration (CI) pipeline using Jenkins on AWS EC2 instances, integrated with various tools for code quality analysis, build automation, and notifications.

### Technologies:

AWS EC2: Provides the compute resources for running Jenkins, Nexus, and SonarQube.
SonarQube: Analyzes code quality and detects issues.
Checkstyle: A code analysis tool used to ensure coding standards.
Maven: Used for building the project.
Jenkins: The CI server that orchestrates the build and deployment pipeline.
Git: Version control system to manage code changes.
Slack: Sends notifications about build and deployment statuses.
Nexus: Manages and stores artifacts.

## Steps:

Login to AWS Account: Access your AWS account.
Create Key Pair: Generate SSH keys for secure access.
Create Security Group: Define security rules for Jenkins, Nexus, and SonarQube.
Create EC2 Instances: Launch instances for Jenkins, Nexus, and SonarQube with appropriate user data scripts.
Post Installation:
Set up Jenkins and install necessary plugins.
Configure Nexus and set up repositories.
Verify SonarQube installation.
Git:
Create a GitHub repository and migrate your code.
Integrate GitHub with VSCode for development and testing.
Build Job with Nexus Integration: Set up Jenkins jobs that interact with Nexus for artifact management.
GitHub Webhook: Configure webhooks to trigger Jenkins builds on code changes.
SonarQube Server Integration: Integrate SonarQube with Jenkins to perform code quality checks.
Nexus Artifact Upload Stage: Configure Jenkins to upload build artifacts to Nexus.
Slack Notification: Set up Slack notifications for build and deployment statuses.

### CI Architecture:

![ci image](https://github.com/user-attachments/assets/a46c45ec-7047-4b17-8ce2-f373d22e7375)
