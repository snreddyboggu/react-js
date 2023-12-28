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
                    sh 'cd $WORKSPACE; npm install'
                   sh 'cd $WORKSPACE; npm run build'

                }
            }
        }
     
}
