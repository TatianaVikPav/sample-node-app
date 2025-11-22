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
                git url: "${GIT_REPO}", branch: "${GIT_BRANCH}"
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t sample-node-app:latest .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat '''
                set KUBECONFIG=C:\\Users\\pavro\\.kube\\config
                kubectl apply -f k8s-deployment.yaml
                kubectl apply -f k8s-service.yaml
                '''
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
