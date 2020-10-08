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
        stage('Installing Docker Client')
        {
            steps{
                script{
                    def dockerHome = tool 'mydocker'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
                    sh "docker --version"
                }
            }
        }
    }
}