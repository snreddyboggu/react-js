pipeline {
   agent {
     label 'Build-server'
     }
     stages {
       stage ('Checkout') {
           steps {
             node ('Build-server') {
               checkout scm
             }
            }
        }      
          stage ('Build') {
              steps {
                 node ('JenkinsSlave_UI') {
                    sh 'cd $WORKSPACE/UIUX; npm install'
                   sh 'cd $WORKSPACE/UIUX; npm run build'

                }
            }
        }
