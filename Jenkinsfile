pipeline {
    agent any
    tools {
    maven 'maven_home'
    jdk 'java_home'
    }
    environment {
    CATALINA_HOME = "/opt/tomcat-app1/"
    APP_NAME = "Stateful-Tracker.war"
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
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('Stop Tomcat') {
            steps {
                echo 'Stop the Tomcat server'
                sh "/opt/tomcat-app1/bin/shutdown.sh"
                sh "sleep 20"
            }
        }
        stage('Backup of WAR file') {
            steps {
                echo 'I am at WAR file backup stage'
                sh "${CATALINA_HOME}/webapps/WAR-backup.sh"
                sh "rm -rf ${CATALINA_HOME}/webapps/${APP_NAME}"
            }
        }
        stage('Deployment with new WAR file ') {
            steps {
                echo 'Deploying war file'
                deploy adapters: [tomcat8(credentialsId: 'tomcat-login', path: '', url: 'http://localhost:8084')], contextPath: '/opt/tomcat-app1/webapps', war: '**/*.war'
                sh "mv *SNAPSHOT.war ${APP_NAME}"
            }
        }
            stage('Start Tomcat') {
            steps {
                echo 'Start the Tomcat server'
                sh "/opt/tomcat-app1/bin/startup.sh"
                sh "sleep 20"
            }
        }
         stage('Application Deployment completed') {
            steps {
                echo 'Application Deployment completed'
            }
          }
        }
    }

