# Jenkins Server Setup in RedHat Linux VM #

## Step - 1 : Create Linux VM ##

1) Create RedHat VM using AWS EC2 (t2.medium) <br/>
2) Enable 8080 Port Number in Security Group Inbound Rules
3) Connect to VM using MobaXterm

## Step-2 : Instal Java ##

```
sudo yum update
sudo subscription-manager register --username=<your-username>
## Verify and Refresh Registration
sudo subscription-manager status
sudo subscription-manager refresh
## Attach a Subscription
sudo subscription-manager attach --auto
## List Enabled Repositories
yum repolist enabled
## This command gives root privileges that allows reading the necessary certificate files
sudo yum list available | grep openjdk
## RHEL 10 appears to provide only the latest OpenJDK version—Java 21
sudo yum install java-21-openjdk
## Install git
sudo yum install git 
java -version
```

## Step-3 : Install Jenkins ##
```
## Import the Jenkins GPG Key
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
## Add Jenkins Yum Repository
sudo tee /etc/yum.repos.d/jenkins.repo <<EOF
[jenkins]
name=Jenkins-stable
baseurl=https://pkg.jenkins.io/redhat-stable
gpgcheck=1
gpgkey=https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
EOF
## update repositories
sudo yum update
## Install Jenkins
sudo yum install jenkins
```

## Step-4 : Start Jenkins ## 

```
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

## Step-5 : Verify Jenkins ##

```
sudo systemctl status jenkins
```
	
## Step-6 : Open jenkins server in browser using VM public ip ##

```
http://public-ip:8080/
```

## Step-7 : Copy jenkins admin pwd ##
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
	   
## Step-8 : Create Admin Account & Install Required Plugins in Jenkins ##


### Uninstalling Jenkins from Red Hat VM ###

## Step-9 : To Stop the Jenkins service from Red Hat ##
```
sudo systemctl stop jenkins

```
## Step-10 :  Remove Jenkins using yum ##
```
sudo yum remove jenkins
```
## Step-11 : Remove Jenkins workspace and configuration ##
```
sudo rm -rf /var/lib/jenkins
```


