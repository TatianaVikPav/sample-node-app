pipeline {
    agent any

    environment {
        IMAGE_NAME = "sample-node-app:latest"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/TatianaVikPav/sample-node-app.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t sample-node-app:latest .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
                sh 'kubectl apply -f k8s-service.yaml'
            }
        }
    }
}
