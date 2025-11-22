pipeline {
    agent any

    environment {
        IMAGE_NAME = "sample-node-app:latest"
        GIT_REPO = "https://github.com/TatianaVikPav/sample-node-app.git"
        GIT_BRANCH = "main"
    }

    stages {
        stage('Checkout Code') {
            steps {
                // ещё раз явно чекаутим репо
                git url: "${GIT_REPO}", branch: "${GIT_BRANCH}"
            }
        }

        stage('Build Docker Image') {
            steps {
                // ВАЖНО: на Windows используем bat, а не sh
                bat 'docker build -t sample-node-app:latest .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Тоже bat
                bat 'kubectl apply -f k8s-deployment.yaml'
                bat 'kubectl apply -f k8s-service.yaml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully ✅'
        }
        failure {
            echo 'Pipeline failed ❌'
        }
    }
}
