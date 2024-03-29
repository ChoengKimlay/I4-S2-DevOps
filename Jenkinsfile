pipeline {
    agent any

    environment {
        BOT_TOKEN = '6288151605:AAH6UsaVEhpzxgVWdQ7ZEJp1yFFz0e8HMtg'
        CHAT_ID = '-1002142257134'
    }

    stages {
        stage('Git Checkout') {
            steps {
                echo 'Code checkout.'
                git branch: 'Midterm', url: 'https://github.com/ChoengKimlay/testJenkins.git'
            }
        }
        stage('Build App') {
            steps {
                echo 'Building...'
                sh "gradle clean build"
            }
        }
        stage('Testing App') {
            steps {
                echo 'Testing...'
                sh "gradle test"
            }
        }
    }

    post {
        success {
            sh '''
                bash scripts/deployment.sh SUCCESS🟢
            '''
        }
        failure {
            sh '''
                bash scripts/deployment.sh FAILED🔴
            '''
        }
    }
}
