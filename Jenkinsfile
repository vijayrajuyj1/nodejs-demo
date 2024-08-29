pipeline {
    agent {
        label 'java-build-node'
    }
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-cred')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            echo 'Checking out the code...'
            git 'https://github.com/vijayrajuyj1/nodejs-demo.git'
           sh ' echo passed'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t vijayarajult2/nodeapp3:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push vijayarajult2/nodeapp3:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
