pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Deploy War To Tomcat'){
            steps{
                sshagent(['private-key']) {
                    script{
                    def mavenPom = readMavenPom file: 'pom.xml'
                    sh "scp 'file: "target/simple-app-${mavenPom.version}.war" /opt/"
                    }
    
                }
                
            }
        }
    }
}
