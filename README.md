
#### Jenkins CI
### Project Overview:




### Technologies 
- AWS EC2       --> Compute resource
- SonarQube    --> Code Analysis server
- CHECKSTYLE   --> Code analysis tool
- Maven        --> Build tool
- Jenkins      --> as a continuous integration server
- GIT          --> Version control system
- Slack        --> Notification
- Nexus        --> Artifact /software repository
  
### Steps:
1. Login to AWS Account 2. Create key pair
3. Create Security Group
a. Jenkins, Nexus & Sonarqube
4. Create Ec2 Instances with userdata a. Jenkins, Nexus & Sonarqube
5. Post installation
a. Jenkins setup & plugins
b. Nexus setup & repository setup c. Sonarqube login test
6. Git
a. Create a GitHub repository & migrate code b. Integrate GitHub repo with VsCode and test it
7. Build a Job with Nexus integration
8. Github Webhook
9. Sonarqube server integration stage
10. Nexus Artifact upload stage
11. Slack Notification

### CI Architecture:

![ci image](https://github.com/user-attachments/assets/a46c45ec-7047-4b17-8ce2-f373d22e7375)
