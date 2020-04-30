pipeline {

    agent any

    stages {

      

                     
     

        stage ('Artifactory configuration') {

            steps {

                rtServer (

                    id: "ARTIFACTORY_SERVER",

                    url: "https://dincric.jfrog.io/artifactory",

                    credentialsId: 'jfrog'
                

                )



                rtMavenDeployer (

                    id: "MAVEN_DEPLOYER",

                    serverId: "ARTIFACTORY_SERVER",

                    releaseRepo: "libs-release-local",

                    snapshotRepo: "libs-snapshot-local"

                )



                rtMavenResolver (

                    id: "MAVEN_RESOLVER",

                    serverId: "ARTIFACTORY_SERVER",

                    releaseRepo: "libs-release",

                    snapshotRepo: "libs-snapshot"

                )

            }

        }

        stage('build and package') {
            steps {
                rtMavenRun (
                    tool: 'maven',
                     pom: 'pom.xml',
                    goals: 'clean install package',
                    deployerId: "MAVEN_DEPLOYER",
                    resolverId: "MAVEN_RESOLVER"
                    )
            }
        }
        
        
    
        
         
                       


       

        
         stage('deploy ') {
       steps {
           
           script {
        sh  'cp /home/dineshreddy99077/frog/jpetstore-6.0.3-SNAPSHOT.war /home/dineshreddy99077/noida/apache-tomcat-7.0.103/webapps/'
               }
        }
               
        }



     

    }

}
