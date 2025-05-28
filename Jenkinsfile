// @Library('Shared') _
pipeline {
    agent any

    environment {
        IMAGE_NAME = "shaheen8954/onlineshop"
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Clone Code') {
            steps {
                clone()
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
               sh 'docker build -t $IMAGE_NAME onlineshop-poc'
            }
        }

        stage('Push to DockerHub') {
            steps {
               sh 'docker push $IMAGE_NAME'

            }
        }

        stage('Run Container') {
            steps {
                // Stop and remove any previous container with same image
                sh '''
                    docker rm -f onlineshop-container || true
                    docker run -d --name onlineshop-container -p 3002:80 $IMAGE_NAME
                '''
            }
        }

        stage('Greeting') {
            steps {
                echo 'Application deployed successfully!'
            }
        }
    }
}
