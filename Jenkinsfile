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
        slackSend(
            message: "✅ Build SUCCESS",
            webhookUrl: credentials('slack-webhook')
        )
    }
    failure {
        slackSend(
            message: "❌ Build FAILED",
            webhookUrl: credentials('slack-webhook')
        )
    }
}