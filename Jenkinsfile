pipeline {
    environment{
        registry = "prajjawalbanati/my-node-app"
        registryCredential = "dockerhub"
        dockerImage=''
    }
    agent {
        docker{
            image 'node:latest'
        }
    }
    stages{
        stage('Cloning Git')
        {
            steps{
                git 'https://github.com/PrajjawalBanati/my-node-app'
            }
        }
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }

        stage('Building Image') { 
            steps {
                script{
                    docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Pushing Image') { 
            steps {
                script{
                        docker.withRegistry('',registryCredential){
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}