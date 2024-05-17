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
                script {
                    def mavenPom = readMavenPom file: 'pom.xml'
         sshagent(['targetnode-cred']) {
             sh "echo $This is version ${mavenPom.version} picking from pom.xml file"
         sh "scp -o StrictHostKeyChecking=no target/*-${mavenPom.version}.war ec2-user@ec2-3-91-44-157.compute-1.amazonaws.com:/opt/"
                  }
               }
            }    
        }
    }
}
