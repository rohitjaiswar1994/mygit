pipeline {
    agent { label 'built-in' }
    environment {
        KUBECONFIG = credentials('kubeconfig')  // Must exist in Jenkins
    }
    stages {
        stage('Test Kubernetes Access') {
            steps {
                sh 'kubectl get pods --all-namespaces'
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}
