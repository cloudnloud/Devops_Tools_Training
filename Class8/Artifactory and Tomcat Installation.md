To start this handson lab,you need following resources.

- 1. Google cloud (or any other cloud or some VM's from your local machine).
- 2. Tomcat VM should have 2 CPU / 4 GB memory / 40 gb Disk. Install Tomcat in **Ubuntu 20 LTS OS machine.
- 3. Class 6 and Class 7 must be completed and ready
- 4. Make sure you have root access or root login credentials.
- 5. For this Tomcat and Artifactory VM you must have 2 CPU and minimum 7.5 GB memory.Create this VM with **Ubuntu 20 LTS OS ** OS machine

*******************************************************************************************************************
- Step 1 : Install pre-requisite software packages
- Step 2 : Configure environment variables
- Step 3: Configure Artifactory and TOMCAT Software Repository
- Step 4: Install Artifcatory
- Step 5: Change Java Heap Size
- Step 6: Install TOMCAT Web Application server
- Step 7: Restart Tomcat and Artifactory Services
- Step 8: Create new pipeline and enable manual deployment to deploy application in tomcat web application server
- Step 9: Create new pipeline and enable auto deployment to deploy application in tomcat web application server


*******************************************************************************************************************

Artifactory

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
*******************************************************************************************************************
## Step 3: Configure Artifactory and TOMCAT Software Repository

just refernece - https://jfrog.com/community/download-artifactory-oss/

```
wget https://releases.jfrog.io/artifactory/artifactory-rpms/artifactory-rpms.repo 
mv artifactory-rpms.repo  /etc/yum.repos.d/
```

Note ::::::
{1)After giving wget https://releases.jfrog.io/artifactory/artifactory-rpms/artifactory-rpms.repo -O jfrog-artifactory-rpms.repo you are able to see Saving to: ‘jfrog-artifactory-rpms.repo’
2) cat /etc/yum.repos.d/jfrog-artifactory-rpms.repo (take base url and check in web browser you can seel all repo)
3)now you aee able to see jfrog artifactory }

## to ensure the repo is configured

- yum repolist

*******************************************************************************************************************

## Step 4: Install Artifcatory
```
sudo yum update && sudo yum install jfrog-artifactory-oss
```
*******************************************************************************************************************
## Step 5: Change Java Heap Size

```
vim /opt/jfrog/artifactory/app/bin/artifactory.default --> Just for reference
```
change heap size to 512mb --> if you want play in testing this also just for reference

*******************************************************************************************************************
## Step 6: Install TOMCAT Web Application server
```
mkdir /usr/local/tomcat
sudo wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.90/bin/apache-tomcat-9.0.90.tar.gz
sudo tar xvf apache-tomcat-9.0.90.tar.gz --strip-components=1 -C /usr/local/tomcat
sudo ln -s /usr/local/tomcat/apache-tomcat-9.0.90 /usr/local/tomcat/tomcat
sudo useradd -r tomcat
sudo chown -R tomcat:tomcat /usr/local/tomcat
```

### Configure the tomcat service
```
vim /etc/systemd/system/tomcat.service
```

```
[Unit]
Description=Apache Tomcat Web Application Container
After=network.target
[Service]
Type=forking
User=tomcat
Group=tomcat
Environment="JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64"
Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom -Djava.awt.headless=true"
Environment="CATALINA_BASE=/usr/local/tomcat"
Environment="CATALINA_HOME=/usr/local/tomcat"
Environment="CATALINA_PID=/usr/local/tomcat/temp/tomcat.pid"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"
ExecStart=/usr/local/tomcat/bin/startup.sh
ExecStop=/usr/local/tomcat/bin/shutdown.sh
[Install]
WantedBy=multi-user.target
```

save the file and exit.Now run the below commands
--------------------------------------------------------
```
systemctl daemon-reload
systemctl enable tomcat
systemctl start tomcat
systemctl status tomcat
```

--------------------------------------------------------------------
```
vim /usr/local/tomcat/conf/tomcat-users.xml
```

```
<role rolename="tomcat"/>
<role rolename="manager-gui"/>
<user username="tomcat" password="s3cret" roles="tomcat,manager-gui,manager-script"/>
```


save the file and exit
------------------------------------------------------------
comment the lines in the below file

```
vim /usr/local/tomcat/webapps/manager/META-INF/context.xml
```

```
 <!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
       allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->
	   
```

save the file and exit.Now run the below commands

```
systemctl daemon-reload
systemctl enable tomcat
systemctl stop tomcat
systemctl start tomcat
systemctl status tomcat
```
-----------------------------------------------------------------------------------------------------
now access the tomcat admin url

- access tomcat console 

http://<linux machine ip address>:8080/
	
- click manager App icon

![image](/images/tomcat-console.png)

- username - tomcat
- password - s3cret


*******************************************************************************************************************
## Step 7: Restart Tomcat and Artifactory Services

```
systemctl restart artifactory;systemctl enable artifactory;systemctl enable tomcat;systemctl restart tomcat
```



http://<linux machine ip address>:8081/artifactory/

*******************************************************************************************************************

## Step 8: Create new pipeline and enable manual deployment to deploy application in tomcat web application server
## Step 9: Create new pipeline and enable auto deployment to deploy application in tomcat web application server


---------------------------------------------------------------------

- [https://github.com/VivekkadamGit/hello-world-jenkins.git](https://github.com/vijaymentor/hello-world-jenkins.git)

- this above git repo is working in java 11

- after we build we get the webapp.war.

- webapp.war

- http://34.69.104.87:8080/webapp/
