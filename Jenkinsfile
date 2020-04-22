pipeline {

    agent any

    stages {

        stage ('Clone') {

            steps {

                git branch: 'master', url: "https://github.com/dinrag/jpetstore-6.git"

            }

        }
                     
       
        
        
     
        




        stage ('Artifactory configuration') {

            steps {

                rtServer (

                    id: "ARTIFACTORY_SERVER",

                    url: "https://dincric.jfrog.io/artifactory",

                   // credentialsId: CREDENTIALS
                    username: 'admin',
    password: 'A@runa11'

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

     

        stage ('Exec Maven') {

            steps {

                rtMavenRun (

                    tool: maven  // Tool name from Jenkins configuration

                  //  pom: 'jpetstore/pom.xml',

                    goals: 'clean install',

                    deployerId: "MAVEN_DEPLOYER",

                    resolverId: "MAVEN_RESOLVER"

                )

            }

        }



        stage ('Publish build info') {

            steps {

                rtPublishBuildInfo (

                    serverId: "ARTIFACTORY_SERVER"

                )

            }

        }
        
       



     

    }

}
