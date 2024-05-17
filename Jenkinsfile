pipeline {
    agent any
    tools {
        maven 'Maven3'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Deploy to Tomcat') {
            steps {
         sshagent(['private-key']) {
         sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@172.31.57.217:/opt/apache-tomcat-10.1.24/webapps/'
              }
           }
        }    
    }
}
