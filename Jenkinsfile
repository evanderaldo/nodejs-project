pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('evanderaldo-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/evanderaldo/nodejs-project.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t olympusgbeme/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push olympusgbeme/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

