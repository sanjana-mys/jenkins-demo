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
            webhookUrl: credentials('slack-webhook'),
            message: "🚀 Build SUCCESS from Jenkins"
        )
    }
    failure {
        slackSend(
            webhookUrl: credentials('slack-webhook'),
            message: "❌ Build FAILED from Jenkins"
        )
    }
}