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

                sh "curl -fsSLO https://get.docker.com/builds/Linux/x86_64/docker-17.04.0-ce.tgz \
&& tar xzvf docker-17.04.0-ce.tgz \
 && sudo mv docker/docker /usr/local/bin \
  && rm -r docker docker-17.04.0-ce.tgz"

            }
        }
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
                    dockerImage=docker.build registry + ":$BUILD_NUMBER"
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