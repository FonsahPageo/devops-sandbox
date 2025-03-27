pipeline {
    agent{ label 'testing' }
    // environment {
    //     // Inject your kubeconfig as a secure credential.
    //     // KUBECONFIG = credentials('kubeconfig-id')
    // }
    stages {
        stage('Checkout') {
            steps {
                sh 'rm -rf devops-sandbox'
                sh 'git clone https://github.com/FonsahPageo/devops-sandbox.git'
            }
        }
        stage('Deploy on docker-compose') {
            steps {
                sh '''
                    cd devops-sandbox/docker_compose
                    docker login
                    echo "Testing123" | sudo -S systemctl start docker
                    echo "Testing123" | sudo -S docker-compose up -d
                '''
            }
        }
        // stage('Deploy to Staging') {
        //     steps {
        //         // Apply the staging overlay (which uses NodePort services)
        //         sh 'kubectl apply -k DEVOPS/overlays/staging'
        //     }
        // }
        // stage('Run Tests') {
        //     steps {
        //         // Run any integration tests or health checks against staging.
        //         sh './run-tests.sh'
        //     }
        // }
        // stage('Production Approval') {
        //     steps {
        //         // Pause the pipeline until a manual approval is given.
        //         input message: 'Proceed to deploy to production?'
        //     }
        // }
        // stage('Deploy to Production') {
        //     steps {
        //         // Apply the production overlay (which uses LoadBalancer services via MetalLB)
        //         sh 'kubectl apply -k DEVOPS/overlays/production'
        //     }
        // }
    }
}

