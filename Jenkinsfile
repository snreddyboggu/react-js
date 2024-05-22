pipeline {
    agent any

    environment {
        REPO = 'ankit20000/react-js'
        REGISTRY = 'ankit20000' // Replace with your DockerHub username
        IMAGE_NAME = 'react-js'
        EKS_CLUSTER_NAME = 'eks-dev-cluster'// Replace with your EKS cluster name
        KUBECONFIG_CREDENTIALS_ID = 'your-kubeconfig-credentials-id' // Jenkins credentials ID for kubeconfig
        AWS_REGION = 'ap-south-1' // e.g., us-west-2
    }

    stages {
        stage('Checkout') {
            steps {
                git url: "https://github.com/${env.REPO}.git"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def imageTag = "latest"
                    docker.build("${env.REGISTRY}/${env.IMAGE_NAME}:${imageTag}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    def imageTag = "latest"
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') { // Replace with your DockerHub credentials ID in Jenkins
                        docker.image("${env.REGISTRY}/${env.IMAGE_NAME}:${imageTag}").push()
                    }
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                script {
                    withCredentials([file(credentialsId: "${env.KUBECONFIG_CREDENTIALS_ID}", variable: 'KUBECONFIG')]) {
                        sh 'kubectl apply -f kubernetes/deployment.yaml'
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
        success {
            echo 'Deployment to EKS was successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
