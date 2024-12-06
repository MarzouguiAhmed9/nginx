pipeline {
    agent any
    
    stages {
        stage('Declarative: Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t ahmed20007/ahlawsahla .'
                }
            }
        }
        
        stage('Run Nginx Container') {
            steps {
                script {
                    sh 'docker run -d -p 8089:80 ahmed20007/ahlawsahla'
                }
            }
        }
        
        stage('Push Image to Docker Registry') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'f68cafe3-147c-4939-8060-f6d961d92e49', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    script {
                        // Login to Docker Hub or your Docker registry using the credentials
                        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        
                        // Push the built image to the correct Docker registry
                        sh 'docker push ahmed20007/ahlawsahla'
                    }
                }
            }
        }
    }
}
