pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = "docker.io"  // Docker registry, default is Docker Hub
        DOCKER_IMAGE = "ahlawsahla"    // The name of your Docker image
        DOCKER_USERNAME = "ahmed20007" // Docker Hub username
        DOCKER_PASSWORD = "SaidaHamdouni2000!" // Docker Hub password
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t "${DOCKER_IMAGE}" .'
                }
            }
        }

        stage('Run Nginx Container') {
            steps {
                script {
                    // Run the Nginx container
                    sh 'docker run -d -p 8089:80 ${DOCKER_IMAGE}'
                }
            }
        }

        stage('Push Image to Docker Registry') {
            steps {
                script {
                    // Log in to Docker Hub
                    withCredentials([usernamePassword(credentialsId: f68cafe3-147c-4939-8060-f6d961d92e49, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        // Authenticate to Docker registry
                        sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'

                        // Push the image to the Docker registry (Docker Hub in this case)
                        sh 'docker push ${DOCKER_IMAGE}'
                    }
                }
            }
        }
    }
}
