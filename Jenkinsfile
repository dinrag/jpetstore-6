pipeline {

    agent any

    stages {
        
        

        

       
      stage('Package') {  
          steps{
    xldCreatePackage artifactsPath: 'target/', manifestPath: 'deployit-manifest.xml', darPath: 'jpetstore-1.0.9.dar'  
  } 
      }
  stage('Publish') {  
      steps{
    xldPublishPackage serverCredentials: 'xl-deploy', darPath: 'jpetstore-1.0.9.dar'
  }  
  }
  stage('Deploy') {  
      steps{
    xldDeploy serverCredentials: 'xl-deploy', environmentId: 'Environments/NGK/ngk1', packageId: 'Applications/jpetstore/1.0.9.'
  }  
  }
     
    }
}
