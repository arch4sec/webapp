pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    
    stages{
        stage('Initialize'){
            steps{
                sh ''' 
                        echo "PATH = ${PATH}"
                        echo "M2_HOME = ${M2_HOME}"
                    '''             
            }
        }
        stage('Check-Git-Secrets'){
            steps{
                sh 'rm trufflehog || true'
                sh 'docker run gesellix/trufflehog --json https://github.com/arch4sec/webapp.git > trufflehog'
                sh 'cat trufflehog'
            }
        }
        stage ('SAST'){
        steps{
            withSonarQubeEnv('sonar') {
			sh 'mvn sonar:sonar'
			sh 'cat target/sonar/report-task.txt'
		       }
            }
        }
        stage ('Build'){
            steps{
            sh 'mvn clean package'
            }
        }
        stage ('Deploy-toTomcat'){
            steps{
                sshagent(['tomcat']){
                    sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@34.249.82.0:/home/ubuntu/prod/apache-tomcat-8.5.57/webapps/webapp.war'
                }
                
            }
        }
	stage ('DAST'){
        steps{
                sh 'docker run -t owasp/zap2docker-stable zap-baseline.py -t http://34.249.82.0:8080/webapp/'
            }
        }
    }
}
