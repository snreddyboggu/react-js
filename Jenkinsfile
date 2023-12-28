pipeline {
   agent {
     label 'Build-server'
     }
     stages {
        stage ('Checkout') {
           steps  {
               checkout scm
             }
            }     
        stage ('Dependency-installation') {
              steps {
                    sh 'cd $WORKSPACE; npm install'

                }
            }
         stage ('Building') {
              steps {
                sh 'cd $WORKSPACE; npm run build'
           }
       } 
       stage ('Deploying to nginx') {
         steps {
                node('Build-server'){
                sh 'sudo ansible-playbook /opt/deploy.yaml'   
       
                }
         }
       }
 }
     
}
