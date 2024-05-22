pipeline{
  agent any

  parameters{
    choice(name: 'action', choices: 'create\ndestroyekscluster', description: 'create/update or destroy the eks cluster')
    string(name: 'cluster', defaultValue: 'eks-dev-cluster', description: 'eks cluster name' )
    string(name: 'region', defaultValue: 'ap-south-1', description: 'eks cluster region')
  }
  
  
  stages{
    
    stage('git checkout'){
      steps{
        git 'https://github.com/snreddyboggu/react-js.git'
      }
    }
    stage('eks connect'){
      steps{
        """ 
                aws eks update-kubeconfig --region ${params.region} --name ${params.cluster}

              """
      }
    }


    stage('eks deployment'){
        when { expression { params.action == 'create'}}
        steps{
          
          scripts{
            def apply = false
            try{
              input message: 'please confirm the apply to initiate the deployment', ok: 'Ready to apply the config'
              apply = true
            }
            catch(error){
              apply = false
              CurrentBuild.result= 'UNSTABLE'
            }
            if(apply){
              sh 
              
            }
         }
      }     
}
