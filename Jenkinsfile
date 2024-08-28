pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-cred')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
          //  git 'https://github.com/ravdy/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t vijayarajult2/nodeapp2:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push vijayarajult2/nodeapp2:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

