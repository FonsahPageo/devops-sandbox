pipeline {
    agent any
    environment {
        // Inject your kubeconfig as a secure credential.
        KUBECONFIG = credentials('kubeconfig-id')
    }
    stages {
        stage('Checkout') {
            steps {
                // Clone your repository containing the Kustomize directory structure.
                git 'https://github.com/FonsahPageo/devops-sandbox.git'
            }
        }
        stage('Deploy to Staging') {
            steps {
                // Apply the staging overlay (which uses NodePort services)
                sh 'kubectl apply -k DEVOPS/overlays/staging'
            }
        }
        stage('Run Tests') {
            steps {
                // Run any integration tests or health checks against staging.
                sh './run-tests.sh'
            }
        }
        stage('Production Approval') {
            steps {
                // Pause the pipeline until a manual approval is given.
                input message: 'Proceed to deploy to production?'
            }
        }
        stage('Deploy to Production') {
            steps {
                // Apply the production overlay (which uses LoadBalancer services via MetalLB)
                sh 'kubectl apply -k DEVOPS/overlays/production'
            }
        }
    }
}

0cv2rc.uzgzeasiazryzelt