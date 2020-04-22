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



   /*     stage ('Exec Maven') {

            steps {

                rtMavenRun (

                    tool: maven, // Tool name from Jenkins configuration

                   pom: 'jpetstore-6/pom.xml',

                    goals: 'clean install package',

                    deployerId: "MAVEN_DEPLOYER",

                    resolverId: "MAVEN_RESOLVER"

                )

            }

     */  
        stage ('deploy') {
            steps { 
    rtUpload (
    serverId: 'ARTIFACTORY_SERVER',
    specPath: '/var/lib/jenkins/workspace/jfrog-jenkins/target',
    failNoOp: true,
 
    // Optional - Associate the uploaded files with the following custom build name and build number.
    // If not set, the files will be associated with the default build name and build number (i.e the 
    // the Jenkins job name and number).
    buildName: 'jfrog-jenkins',
    buildNumber: '11'
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
