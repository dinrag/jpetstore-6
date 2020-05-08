pipeline {

    agent any

    stages {
        
        

        

       
      stage('Package') {  
          steps{
    xldCreatePackage artifactsPath: 'target/', manifestPath: 'deployit-manifest.xml', darPath: 'jpetstore-1.1.0.dar'  
  } 
      }
  stage('Publish') {  
      steps{
    xldPublishPackage serverCredentials: 'dinesh', darPath: 'jpetstore-1.1.0.dar'
  }  
  }
  stage('Deploy') {  
      steps{
    xldDeploy serverCredentials: 'dinesh', environmentId: 'Environments/DINDEV/dinesh', packageId: 'Applications/jpetstore/1.1.0'
  }  
  }
     
    }
}
