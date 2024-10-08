# DevOps-Project-kubernetes-tomcat-session-replication

![image](https://github.com/user-attachments/assets/5e9d8380-300b-42fc-bf31-a5d4c8940bd1)

This project explains tomcat based session replication in Kubernetes. To achieve this I have used redission based session replication. 
```
I have added below section in context.xml as shown in the screeshot below.


    <Manager className="org.redisson.tomcat.RedissonSessionManager"
    configPath="${catalina.base}/redisson.yaml"
    readMode="REDIS" updateMode="DEFAULT" broadcastSessionEvents="false"
    keyPrefix="" />
```
![image](https://github.com/user-attachments/assets/6bdbb9fa-d260-4695-8b85-063634e3aa37)

I have downloaded the jar file **redisson-all-3.22.0.jar** and **redisson-tomcat-8-3.22.0.jar** from the link https://repo1.maven.org/maven2/org/redisson/redisson-all/3.22.0/redisson-all-3.22.0.jar and https://repo1.maven.org/maven2/org/redisson/redisson-tomcat-8/3.22.0/redisson-tomcat-8-3.22.0.jar. Download these two jar files to the lib directory. You can refer the **Dockerfile** as shown in the screenshot below.
```
FROM tomcat:8-jdk11-openjdk 

MAINTAINER "DevOps Team"

ADD https://repo1.maven.org/maven2/org/redisson/redisson-all/3.22.0/redisson-all-3.22.0.jar /usr/local/tomcat/lib/
ADD https://repo1.maven.org/maven2/org/redisson/redisson-tomcat-8/3.22.0/redisson-tomcat-8-3.22.0.jar /usr/local/tomcat/lib/

COPY ./pasco/context.xml /usr/local/tomcat/conf/
COPY ./pasco/redisson.yaml /usr/local/tomcat/

COPY target/ROOT.war /usr/local/tomcat/webapps
```
For Jenkins you should install the plugins 1. SonarQube Scanner 2. Nexus Artifact Uploader and 3. Pipeline Utility Steps as shown in the screenshot below.

![image](https://github.com/user-attachments/assets/d8869bd8-ec81-407a-967e-ee8cc29d6443)

After adding the Jenkins Slave node the screenshot is as shown below.
![image](https://github.com/user-attachments/assets/5fc46e75-94e8-4bcf-bf14-6d42b602b0f6)

commands to add swap space of 512 MB is given below
```
fallocate -l 512M /swapfile
chmod 600 /swapfile
sudo mkswap /swapfile
cat /etc/fstab

/swapfile swap swap defaults 0 0


swapon /swapfile
free -mh

```
![image](https://github.com/user-attachments/assets/27933e3f-1631-469d-a08a-01803965efa2)

To run the Jenkins Job successfully webhook had been created in SonarQube and modified the /etc/resolv.conf file on SonarQube and on Jenkins Slave Node as shown in the screenshot below (You can also achieve this by creating a new DHCP option set, I had already discussed regarding this in earlier project You can refer https://github.com/kamalmohan217/DevOps-Project-2tier-WebApp-Deployment/blob/main/Complications-which-you-may-face/complications.md ).
![image](https://github.com/user-attachments/assets/39defa93-3a49-4006-b326-7a6067c6b661)
![image](https://github.com/user-attachments/assets/7d62974e-7987-4d97-833a-f7191aa5cb2e)
![image](https://github.com/user-attachments/assets/7f180eef-7e35-4dba-923b-797ccaa6c40e)

The screenshot of Jenkins Job is as shown below.
![image](https://github.com/user-attachments/assets/66c05fe7-5087-4725-a6ae-cf9edd2bed1d)

The screenshots of SonarQube, Nexus Artifactory, ArgoCD and Route53 record set entry after successfully running the Jenkins Job is as shown in the screenshot below.
![image](https://github.com/user-attachments/assets/f773cb18-2145-4a1b-9298-46cf2fc36ca8)
![image](https://github.com/user-attachments/assets/7a657ead-d794-46a4-8717-8a18aa540fcc)
![image](https://github.com/user-attachments/assets/17f68ecd-eedc-4f56-bd7e-97f415cc444e)
![image](https://github.com/user-attachments/assets/8eb294c9-c78c-4b4e-b4f6-b4daac3dad5e)

The Session Id shown in the below screenshot confirms the session replication.
![image](https://github.com/user-attachments/assets/30fb8423-c7cb-44fb-90f9-b5a7cb998bc3)
![image](https://github.com/user-attachments/assets/35ed2aeb-e66d-43d0-bbc1-53cf76a91c63)


<br><br/>
<br><br/>
<br><br/>
<br><br/>
<br><br/>
```
Source Code:-  https://github.com/kamalmohan217/kubernetes-tomcat-session-replication.git
```
<br><br/>
<br><br/>
<br><br/>
<br><br/>
<br><br/>
```
References:-  https://github.com/AndriyKalashnykov/tomcat-root-war.git
             https://redisson.org/articles/redis-based-tomcat-session-management.html
             https://github.com/mahendra-shinde/tomcat7-redisson-session.git
             https://github.com/bitnami/charts.git
```
