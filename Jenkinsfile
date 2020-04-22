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

                    id: "Artifactory",

                    url: https://dincric.jfrog.io/artifactory,

                    credentialsId: CREDENTIALS

                )



                rtMavenDeployer (

                    id: "MAVEN_DEPLOYER",

                    serverId: "Artifactory",

                    releaseRepo: "libs-release-local",

                    snapshotRepo: "libs-snapshot-local"

                )



                rtMavenResolver (

                    id: "MAVEN_RESOLVER",

                    serverId: "Artifactory",

                    releaseRepo: "libs-release",

                    snapshotRepo: "libs-snapshot"

                )

            }

        }



        stage ('Exec Maven') {

            steps {

                rtMavenRun (

                    tool: maven, // Tool name from Jenkins configuration

                    pom: 'jpetstore-6/pom.xml',

                    goals: 'clean install',

                    deployerId: "MAVEN_DEPLOYER",

                    resolverId: "MAVEN_RESOLVER"

                )

            }

        }



        stage ('Publish build info') {

            steps {

                rtPublishBuildInfo (

                    serverId: "Artifactory"

                )

            }

        }

    }

}
