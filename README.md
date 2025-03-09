# Jenkins Installation
- Go to AWS Console
- Instances(running)
- Launch instance
![image](https://github.com/user-attachments/assets/4dbcc8ef-b4ec-4416-9606-643e61f9083f)

# Install Jenkins
- Java(JDK) is Pre-requisite

# Run the below commands to install Java and Jenkins
- Install Java
  sudo apt update
  sudo apt install openjdk-17-jre

   Verify Java installed or not
    java --version
 
  Now, you can proceed with installing Jenkins
      curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \ /usr/share/keyrings/jenkins-keyring.asc > /dev/null echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \ https://pkg.jenkins.io/debian binary/ | sudo tee \  /etc/apt/sources.list.d/jenkins.list > /dev/null sudo apt-get update sudo apt-get install jenkins

  **Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

  - EC2 > Instances > Click on
  - In the bottom tabs -> Click on Security
  - Security groups
  - Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).
 
    Then Open Publicip:8080 in chrome

    You will se the Jenkins page waiting for some password

    sudo cat /var/lib/jenkins/secrets/initialAdminPassword in your terminal.

    Copy the password from terminal to chrome and start installing selected plugins
    ![image](https://github.com/user-attachments/assets/02fe020c-b76d-4f2c-a962-c7cc43f12c74)

    Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]

    Jenkins Installation is Successful. You can now starting using the Jenkins

    ![image](https://github.com/user-attachments/assets/1f8206de-31a9-46b4-b8c9-86ede49a959f)

# Install the Docker Pipeline plugin in Jenkins:
  - Log in to Jenkins.
  - Go to Manage Jenkins > Manage Plugins.
  - In the Available tab, search for "Docker Pipeline".
  - Select the plugin and click the Install button.
  - Restart Jenkins after the plugin is installed.
    ![image](https://github.com/user-attachments/assets/78d788ae-1569-46b8-8f69-09fae786a5bc)
    
    Wait for the Jenkins to be restarted.

# Docker Slave Configuration
Run the below command to Install Docker

sudo apt update
sudo apt install docker.io

Grant Jenkins user and Ubuntu user permission to docker deamon.

sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker

Once you are done with the above steps, it is better to restart Jenkins.

http://<ec2-instance-public-ip>:8080/restart

The docker agent configuration is now successful.    
