To start this handson lab,you need following resources.

1. Google cloud (or any other cloud or some VM's from your local machine).
2. Jenkins VM should have 2 CPU / 4 GB memory / 40 gb Disk. Also Install **rocky linux 8 and above** OS machine.
3. Make sure you have root access or root login credentials.

*******************************************************************************************************************
- Step 1 : Install pre-requisite software packages
- Step 2 : Configure environment variables
- Step 3: Configure Jenkins Software Repository
- Step 4: Configure Jenkins Key
- Step 5: Install Jenkins
- Step 6: start the Jenkins Service Persistantly
- Step 7: Install the necessary plugins
- Step 8: Global Tools Settings - In Jenkins Console - JAVA , MAVEN, GIT
*******************************************************************************************************************
Step 1 : Install pre-requisite software packages

```
curl -O https://download.java.net/java/GA/jdk11/13/GPL/openjdk-11.0.1_linux-x64_bin.tar.gz
```

```
tar zxvf openjdk-11.0.1_linux-x64_bin.tar.gz
```

```
mv jdk-11.0.1 /usr/local/
```

```
yum install java-11-openjdk-devel
```

```
yum install vim wget  git -y
```

```
systemctl stop firewalld;systemctl disable firewalld
```

```
wget https://archive.apache.org/dist/maven/maven-3/3.8.5/binaries/apache-maven-3.8.5-bin.tar.gz
```


```
tar xvf apache-maven-3.8.5-bin.tar.gz
```

```
mv apache-maven-3.8.5  /usr/local/apache-maven
```

*******************************************************************************************************************
Step 2 : Configure environment variables

vim ~/.bash_profile

In this file



export JAVA_HOME=/usr/local/jdk-11.0.1/
export JRE_HOME=/usr/lib/jvm/jre-11/
PATH=$PATH:$HOME/bin:$JAVA_HOME/bin:$JRE_HOME/bin
export M2_HOME=/usr/local/apache-maven
export M2=$M2_HOME/bin
export PATH=$M2:$PATH


source ~/.bash_profile
*******************************************************************************************************************

Check Maven Build Tool Version

mvn -version


*******************************************************************************************************************
Step 3: Configure Jenkins Software Repository


wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo

*******************************************************************************************************************
Step 4: Configure Jenkins Key


rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
*******************************************************************************************************************
Step 5: Install Jenkins


yum install jenkins -y

*******************************************************************************************************************
Step 6: start the Jenkins Service Persistantly


systemctl restart jenkins;systemctl enable jenkins;systemctl status jenkins
*******************************************************************************************************************


http://<jenkins Server IP >:8080/

[root@master java-1.8.0]# cat /var/lib/jenkins/secrets/initialAdminPassword
9da04e163934413fbb5128977ec567bb

*******************************************************************************************************************

Step 7: Install the necessary plugins

The following plugins needs to be installed

dashboard view
Build Pipeline
Deploy to container
Email Extension Template
*******************************************************************************************************************
Step 8: Global Tools Settings - In Jenkins Console - JAVA , MAVEN, GIT
