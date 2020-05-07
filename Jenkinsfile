pipeline {

    agent any

    stages {
        
        
          stage ('Artifactory configuration') {

            steps {

                rtServer (

                    id: "ARTIFACTORY_SERVER1",

                    url: "https://sakthishivani.jfrog.io/artifactory",

                    credentialsId: 'jfrog'
                

                )



                rtMavenDeployer (

                    id: "MAVEN_DEPLOYER",

                    serverId: "ARTIFACTORY_SERVER1",

                    releaseRepo: "libs-release-local",

                    snapshotRepo: "libs-snapshot-local"

                )



                rtMavenResolver (

                    id: "MAVEN_RESOLVER",

                    serverId: "ARTIFACTORY_SERVER1",

                    releaseRepo: "libs-release",

                    snapshotRepo: "libs-snapshot"

                )

            }

        }

       
      stage('Package') {  
          steps{
    xldCreatePackage artifactsPath: 'libs-snapshot-local/', manifestPath: 'deployit-manifest.xml', darPath: 'jpetstore-1.0.3.dar'  
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
