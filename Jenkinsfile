pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('CHECKOUT') {
            steps {
                git 'https://github.com/sanjana-mys/jenkins-demo.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
    }

  post {
    success {
        withCredentials([string(credentialsId: 'slack-webhook', variable: 'WEBHOOK')]) {
            bat '''
            curl -X POST -H "Content-type: application/json" --data "{\\"text\\":\\"🚀 Jenkins Build SUCCESS\\"}" %WEBHOOK%
            '''
        }
    }
    failure {
        withCredentials([string(credentialsId: 'slack-webhook', variable: 'WEBHOOK')]) {
            bat '''
            curl -X POST -H "Content-type: application/json" --data "{\\"text\\":\\"❌ Jenkins Build FAILED\\"}" %WEBHOOK%
            '''
        }
    }
}