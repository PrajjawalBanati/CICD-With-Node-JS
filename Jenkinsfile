pipeline {
    agent {
        docker {
            image 'node:latest' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                git 'https://github.com/PrajjawalBanati/my-node-app'
                sh 'npm install' 
            }
        }
    }
}