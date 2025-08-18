pipeline {
    agent {
        label 'built-in'  // Replace with your agent label or use 'any'
    }
    environment {
        KUBECONFIG = credentials('kubeconfig')  // Verify credential ID
    }
    stages {
        stage('Test Kubernetes Access') {
            steps {
                script {
                    // Check if kubectl is installed
                    sh '''
                        if ! command -v kubectl &> /dev/null; then
                            echo "ERROR: kubectl not installed!"
                            exit 1
                        fi
                        kubectl get pods --all-namespaces || exit 1
                    '''
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
    post {
        failure {
            echo "Pipeline failed! Check logs."
        }
        success {
            echo "Deployment succeeded!"
        }
    }
}
