pipeline {
    agent any

    environment {
        PATH = "/Applications/Docker.app/Contents/Resources/bin:/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin"
        KUBECONFIG = "/Users/rekhasamhitha/.kube/config"
    }

    stages {
        stage('Connection Check') {
            steps {
                sh 'kubectl cluster-info'
                sh 'kubectl get nodes'
                sh 'kubectl get deployment ecommerce'
            }
        }

        stage('Scale Deployment') {
            steps {
                sh 'kubectl scale deployment/ecommerce --replicas=3'
                sh 'kubectl rollout status deployment/ecommerce --timeout=120s'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'kubectl get deployment ecommerce'
                sh 'kubectl get pods'
            }
        }
    }

    post {
        success {
            echo 'Deployment scaling and verification completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check the stage logs for the error.'
        }
    }
}
