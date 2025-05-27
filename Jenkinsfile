pipeline {
    agent any

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
        stage('build image ') {
            steps {
                sh "docker build -t shaheen8954/onlineshop ."
            }
        }
        stage('run container') {
            steps {
                sh "docker run -d -p 3002:80 shaheen8954/onlineshop"
            }
        }
        stage('greeting ') {
            steps {
                echo "Thank you "
            }
        }
    }
}
