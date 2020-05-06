pipeline {
    agent any

    stages {
        
         stage('Package') { 
             steps {
    xldCreatePackage artifactsPath: 'libs-snapshot-local/',  warPath: 'libs-snapshot-local/org/mybatis/jpetstore/6.0.3-SNAPSHOT/jpetstore-6.0.3-20200506.042637-9.war'  
  }  
         }
  stage('Publish') { 
      steps {
    xldPublishPackage serverCredentials: 'xl-deploy', warPath: 'libs-snapshot-local/org/mybatis/jpetstore/6.0.3-SNAPSHOT/jpetstore-6.0.3-20200506.042637-9.war'
  }  
  }
  stage('Deploy') { 
      steps {
    xldDeploy serverCredentials: 'xl-deploy', environmentId: 'Environments/NGK/ngk1', packageId: 'Applications/jpetstore/1.0.0'
  }  
}
     
    }
}
