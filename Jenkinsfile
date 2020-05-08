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
    xldPublishPackage serverCredentials: 'xl', darPath: 'jpetstore-1.1.0.dar'
  }  
  }
  stage('Deploy') {  
      steps{
    xldDeploy serverCredentials: 'xl', environmentId: 'Environments/NGK/ngk1', packageId: 'Applications/jpetstore/1.1.0.'
  }  
  }
     
    }
}
