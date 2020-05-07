pipeline {

    agent any

    stages {

       
      stage('Package') {  
          steps{
    xldCreatePackage artifactsPath: 'libs-snapshot-local/',manifestPath: 'deployit-manifest.xml', darPath: 'jpetstore-1.0.3.dar'  
  } 
      }
  stage('Publish') {  
      steps{
    xldPublishPackage serverCredentials: 'xl-deploy', darPath: 'jpetstore-1.0.3.dar'
  }  
  }
  stage('Deploy') {  
      steps{
    xldDeploy serverCredentials: 'xl-deploy', environmentId: 'Environments/DEVS/sakthi', packageId: 'Applications/jpetstore/1.0.3.'
  }  
  }
     
    }
}
