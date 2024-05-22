pipeline {
  agent any

  parameters {
    choice(name: 'action', choices: 'create\ndestroy\ndestroyekscluster', description: 'create/update or destroy the eks cluster')
    string(name: 'cluster', defaultValue: 'eks-dev-cluster', description: 'eks cluster name')
    string(name: 'region', defaultValue: 'ap-south-1', description: 'eks cluster region')
  }

  environment {
    ACCESS_KEY = credentials('aws_access_key_id')
    SECRET_KEY = credentials('aws_secret_access_key')
  }

  stages {
    stage('git checkout') {
      steps {
        git 'https://github.com/snreddyboggu/react-js.git'
      }
    }

    stage('eks connect') {
      steps {
        sh """
          aws configure set aws_access_key_id "$ACCESS_KEY"
          aws configure set aws_secret_access_key "$SECRET_KEY"
          aws configure set region "${params.region}"
          aws eks update-kubeconfig --region ${params.region} --name ${params.cluster}
        """
      }
    }

    stage('eks deployment') {
      when {
        expression { params.action == 'create' }
      }
      steps {
        script {
          def apply = false
          try {
            input message: 'Please confirm to apply the configuration to initiate the deployment', ok: 'Apply'
            apply = true
          } catch (error) {
            apply = false
            currentBuild.result = 'UNSTABLE'
          }
          if (apply) {
            sh """
              kubectl apply -f kubernetes/deployment.yaml
            """
          }
        }
      }
    }
    
    // Optionally, add stages for destroy actions if needed
    stage('eks destroy') {
      when {
        expression { params.action == 'destroy' }
      }
      steps {
        script {
          def destroy = false
          try {
            input message: 'Please confirm to destroy the EKS resources', ok: 'Destroy'
            destroy = true
          } catch (error) {
            destroy = false
            currentBuild.result = 'UNSTABLE'
          }
          if (destroy) {
            sh """
              kubectl delete -f kubernetes/deployment.yaml
            """
          }
        }
      }
    }
    
    // Add a stage for destroying the EKS cluster if needed
    stage('destroy eks cluster')
