pipeline {
    agent any 

     options {
        timeout(time: 10, unit: 'MINUTES')
     }
    environment {
    DOCKERHUB_CREDENTIALS = credentials('karo-dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/ooghenekaro/Simple-Nodejs-Docker-application.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t ooghenekaro/node-app:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push ooghenekaro/node-app:$BUILD_NUMBER'
            }
        }
    }
}
