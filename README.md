# CI-CD-ansible-maven-docker-git
Building CD/CD pipeline with Jenkins, Docker, Maven, Ansible, Git.

**Create two server Jenkins & Dev-sever**
configure Jenkins on Jenkins server and also required some tools 
like, git maven, ansible
Install git 
yum install git* -y
Check git 
git --version

Install maven 
Dependencies of maven 
OpenJDK 
The current version is Java 17 but the command yum list -a | grep openjdk shows only available OpenJDK versions are 17 and 21.We will install JDK using binaries and setting some required environment variables.

Download the JDK Binaries
Go to the URL: https://www.oracle.com/java/technologies/downloads/#java17 Copy the download link for Linux/x64 build. Then use the below command to download and extract it.

https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.tar.gz ( sha256)
tar -xvf openjdk-17.0.1_linux-x64_bin.tar.gz
/usr/lib/

Step 2: Setting JAVA_HOME and Path Environment Variables
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
export PATH=$JAVA_HOME/bin:$PATH

Step 3: Verify the Java Installation
java -version
openjdk version "17.0.6-ea" 2023-01-17 LTS
OpenJDK Runtime Environment (Red_Hat-17.0.6.0.9-0.3.ea.el8) (build 17.0.6-ea+9-LTS)
OpenJDK 64-Bit Server VM (Red_Hat-17.0.6.0.9-0.3.ea.el8) (build 17.0.6-ea+9-LTS, mixed mode, sharing)

Installing Maven on Linux/Centos
We will install Maven in a similar way that we have installed JDK in the Linux system.

Step 1: Download the Maven Binaries
Go to the URL: https://maven.apache.org/download.cgi Copy the link for the “Binary tar.gz archive” file. Then run the following commands to download and untar it.

wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz
ls
apache-maven-3.9.9-bin.tar.gz 
ls
apache-maven-3.9.9  apache-maven-3.9.9-bin.tar.gz   
 mv apache-maven-3.9.9 /opt/
ls /opt/
apache-maven-3.9.9  cni  containerd  tomcat

Step 2: Setting M2_HOME and Path Variables
Temporary  environment variable path set
export MAVEN_HOME=/opt/apache-maven-3.9.9
export PATH=$MAVEN_HOME/bin:$PATH

Permanent environment variable configure 
Add the following lines to the user profile file (.profile).
vim ~/.bashrc

Set Maven environment variables
export MAVEN_HOME=/opt/apache-maven-3.9.9
export PATH=$MAVEN_HOME/bin:$PATH

Step 3: Verify the Maven installation
mvn -verison
Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937)
Maven home: /opt/apache-maven-3.9.9
Java version: 17.0.6-ea, vendor: Red Hat, Inc., runtime: /usr/lib/jvm/java-17-openjdk-17.0.6.0.9-0.3.ea.el8.x86_64
Default locale: en_IN, platform encoding: UTF-8
OS name: "linux", version: "4.18.0-553.6.1.el8.x86_64", arch: "amd64", family: "unix"

Configure Ansible on Jenkins server (os amazon-Linux)
sudo amazon-linux-extras install ansible2 -y
Check version
ansible --version

Check executable location
which ansible
/usr/bin/ansible

Install plugin on Jenkins dashboard
Dashboard > Manage Jenkins > Plugins > Available plugins > Search available plugins: Ansible plugins > Install > Restart Jenkins when installation is completed and no jobs are running. 
> login to Jenkins Dashboard. 
Dashboard > Manage Jenkins > Tools > Ansible installations > Add Ansible > Name:ansible 
> Path to ansible executables directory: /usr/bin > Apply > Save 

Create pipeline with name java-app-pipeline

iNSTALL DOCKER ON JENKINS MACHINE
yum install docker.io -y 
Add Jenkins user to docker 
usermod -a -G docker jenkins
Restart jenkins
#systemctl restart jenkins.service
Start & enable docker service
systemctl start docker.service
systemctl enable docker.service
systemctl status docker.srevice

