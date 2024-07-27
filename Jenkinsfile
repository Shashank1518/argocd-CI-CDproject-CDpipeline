pipeline{
  agent any
  environment{
    
    APP_NAME = "argocd-ci-cdproject"
    
  }
  stages{


    
      stage('Git checkout'){
        steps{
          script{
            git branch: 'main', url: 'https://github.com/Shashank1518/argocd-CI-CDproject.git'  
          }
        }   
      }
    
      stage('Updating kubernetes deployment file'){
        steps{
          script{
            sh """
              cat deployment.yml
              sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yml
              cat deployment.yml
               """
          }
        }
      }

        stage('Push the changed deployment file to Git'){
          steps{
            script{
              sh """
                git config --global user.name "shashank1518"
                git config --global user.email "shashanklm007@gmail.com" 
                git add deployment.yml
                git commit -m "updated the deployment file"
                 """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                  sh "git push https://github.com/Shashank1518/argocd-CI-CDproject.git main"
                }
            }
          }
        }
    
   
















        
      
    }
}
