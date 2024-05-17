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
         sh 'scp -o StrictHostKeyChecking=no "target/sample-app.${mavenPom.version}.war" ec2-user@ec2-3-91-44-157.compute-1.amazonaws.com:/opt/'
                  }
               }
            }    
        }
    }
}
