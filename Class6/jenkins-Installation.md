To start this handson lab,you need following resources.

1. Google cloud (or any other cloud or some VM's from your local machine).
2. Jenkins VM should have 2 CPU / 4 GB memory / 40 gb Disk. Also Install Rocky linux in this machine.
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
- Step 1 : Install pre-requisite software packages

```
apt update
apt install fontconfig openjdk-17-jre
```

```
apt install vim wget  git -y
```

```
wget https://dlcdn.apache.org/maven/maven-3/3.9.8/binaries/apache-maven-3.9.8-bin.tar.gz
```


```
tar xvf apache-maven-3.9.8-bin.tar.gz
```

```
mv apache-maven-3.9.8  /usr/local/apache-maven
```



*******************************************************************************************************************
- Step 2 : Configure environment variables
```
vim ~/.profile
```

- In this file
```


export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64/
PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
export M2_HOME=/usr/local/apache-maven
export M2=$M2_HOME/bin
export PATH=$M2:$PATH

```

```
source ~/.profile
```


*******************************************************************************************************************

- Check Maven Build Tool Version

```
mvn -version
```

```
java --version
```
**********************************************************************************************************************************


- Step 3: Configure Jenkins Software Repository

```
wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
```

*******************************************************************************************************************
- Step 4: Configure Jenkins Key

```
rpm --import https://pkg.jenkins.io/redhat/jenkins.io-2023.key
```
*******************************************************************************************************************
- Step 5: Install Jenkins
```
yum install jenkins -y
```
*******************************************************************************************************************
- Step 6: start the Jenkins Service Persistantly

```
systemctl restart jenkins;systemctl enable jenkins;systemctl status jenkins
```
*******************************************************************************************************************


http://<jenkins Server IP >:8080/

[root@master java-1.8.0]# cat /var/lib/jenkins/secrets/initialAdminPassword
9da04e163934413fbb5128977ec567bb

*******************************************************************************************************************

- Step 7: Install the necessary plugins

The following plugins needs to be installed

- dashboard view
- Build Pipeline
- Deploy to container
- maven integration
- Email Extension Template
*******************************************************************************************************************
- Step 8: Global Tools Settings - In Jenkins Console - JAVA , MAVEN, GIT
  
**********************************************************************************************************************

  
  https://github.com/cloudnloud/webapplication_demo
