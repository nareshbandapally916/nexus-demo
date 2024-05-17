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
        stage('Deploy to Server'){
            sshagent (credentials: ['private-key']) {
                sh 'ssh -o StrictHostKeyChecking=no target/*.war ec2-user@ec2-3-91-44-157.compute-1.amazonaws.com:/opt/'
               }
        }
    }
}
