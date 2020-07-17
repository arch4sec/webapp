This is a sample Web Application to use during DevSecOps CICD demos.
#Tools
- trufflehog
- OWASP Dependency Check
- SonarQube
- OWASP ZAP

#Build Instruction

```
mvn3 clean package
```
#Check Git secrets with trufflehog
get trufflehog docker image first
```
docker pull gesellix/trufflehog
```
#Deploy instruction

Deploy ```target/WebApp.war``` on Tomcat
 
#TODO
 
Add instruction to deploy to ElasticBeanstalk


:octocat:
