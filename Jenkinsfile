pipeline {
    agent { label 'built-in' }
    environment {
        KUBECONFIG = credentials('kubeconfig')  // Reference your Kubernetes credentials in Jenkins
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/rohitjaiswar1994/mygit.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app:latest .'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    kubectl apply -f k8s-deployment.yaml
                    kubectl rollout status deployment/my-app
                '''
            }
        }
    }
}
