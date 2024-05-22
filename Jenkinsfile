pipeline{
  agent any

  parameters{
    choice(name: 'action', choices: 'create\ndestroyekscluster', description: 'create/update or destroy the eks cluster')
  }
  
  
  stages{
    
    stage('git checkout'){
      steps{
        git 'https://github.com/snreddyboggu/react-js.git'
      }
    stage('eks connect'){
        when{ expression{ params.action == 'create}}
        steps{
          scripts{
            def apply == false
            try:
              
          }
      }      
    }
}
