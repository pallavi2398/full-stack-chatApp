pipeline {
    agent any

    environment {
        KUBE_NAMESPACE = "chatapp"
    }

    stages {

        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/yourusername/full-stack-chatApp.git'
            }
        }

        stage('Deploy MongoDB') {
            steps {
                script {
                    sh "kubectl apply -f k8s-manifests/mongo -n ${KUBE_NAMESPACE}"
                }
            }
        }

        stage('Deploy Backend') {
            steps {
                script {
                    sh "kubectl apply -f k8s-manifests/backend -n ${KUBE_NAMESPACE}"
                }
            }
        }

        stage('Deploy Frontend') {
            steps {
                script {
                    sh "kubectl apply -f k8s-manifests/frontend -n ${KUBE_NAMESPACE}"
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    sh "kubectl get pods -n ${KUBE_NAMESPACE}"
                    sh "kubectl get svc -n ${KUBE_NAMESPACE}"
                }
            }
        }
    }

    post {
        success {
            echo "✅ Full-stack chat app deployed successfully on Kubernetes!"
        }
        failure {
            echo "❌ Deployment failed. Check logs and fix errors."
        }
    }
}
