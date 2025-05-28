pipeline {
    agent any
     environment {
        IMAGE_NAME = "shaheen8954/onlineshop"
    }

    stages {
        stage('Clean Workspace ') {
            steps {
                cleanWs()
            }
        }
        stage('clone code ') {
            steps {
                git url: " https://github.com/Shaheen8954/onlineshop-poc.git", branch: "main"
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
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }

        stage('Run container') {
            steps {
                sh 'docker run -d -p 3002:80 $IMAGE_NAME'
            }
        }

        stage('greeting ') {
            steps {
                echo 'Application deployed successfully!'
            }
        }
    }
}
