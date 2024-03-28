pipeline {
    agent any // windows agent, Jenkins-Laravel (other machine)
    
    stages {
        stage('Fetch from GitHub') { // build steps
            steps {
                echo 'Fetching from GitHub'
                git branch: 'TP03', url:'https://github.com/ChoengKimlay/testJenkins.git'
            }
        }
        stage('Build using Tools') {
            steps {
                echo 'Compiling code...'
                sh 'cp .env.example .env'
                sh 'composer install && php artisan key:generate && npm install && npm run build'
            }
        }
        stage('Test the app') {
            steps {
                echo 'Testing unit tests...'
                echo 'Testing features...'
                sh 'php artisan test'
            }
        }
    }
    
    post {
        success {
            emailext subject: "Pipeline Successful: ${currentBuild.fullDisplayName}",
                     body: "The pipeline ${currentBuild.fullDisplayName} has completed successfully.",
                     to: "mingfongmen@gmail.com"
        }
        failure {
            emailext subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                     body: "The pipeline ${currentBuild.fullDisplayName} has failed. Please check the console output for details.",
                     to: "mingfongmen@gmail.com"
        }
    }
}