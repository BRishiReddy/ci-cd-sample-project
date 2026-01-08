pipeline {
    agent any

    environment {
        DOCKER_HUB_USER = 'yourdockerhubusername'
        IMAGE_NAME = 'ci-cd-sample'
    }

    stages {

        stage('Pull Code') {
            steps {
                git 'https://github.com/yourusername/ci-cd-sample-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_HUB_USER/$IMAGE_NAME:latest .'
            }
        }

        stage('Docker Login') {
            steps {
                sh "echo $DOCKER_HUB_PASS | docker login -u $DOCKER_HUB_USER --password-stdin"
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker push $DOCKER_HUB_USER/$IMAGE_NAME:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}

