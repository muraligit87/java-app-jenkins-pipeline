pipeline {
    agent any
    tools {
    maven 'maven_home'
    jdk 'java_home'
    }

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
                sh "mvn clean compile package"
                
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying war file'
            }
        }
    }
}
