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
        stage ('Build'){
            steps{
            sh 'mvn clean package'
            }
        }
        stage ('Deploy-toTomcat'){
            steps{
                sshagent(['tomcat']){
                    sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@3.250.146.239:/home/ubuntu/prod/apache-tomcat-8.5.57/webapps/webapp.war'
                }
                
            }
        }
    }
}

