pipeline {
   agent {
     label 'slavename-level'
     }
     stages {
       stage ('Checkout') {
           steps {
             node ('BuildNodeNmae') {
               checkout scm
             }
            }
        }      
          stage ('Build') {
              steps {
                 node ('JenkinsSlave_UI') {
                    sh 'cd $WORKSPACE/UIUX; npm install --unsafe-perm'
                   sh 'cd $WORKSPACE/UIUX; npm run build --prod'

                }
            }
        }
