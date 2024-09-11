pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                echo 'I am at build stage'
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'Git', url: 'https://github.com/muraligit87/java-app-jenkins-pipeline.git']])
            }
        }
        stage('Maven build') {
            steps {
                echo 'I am at Maven build stage'
                
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying war file'
                cp *SNAPSHOT.war /opt/tomcat-app1/webapps
            }
        }
    }
}
