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

        
        stage('upload war') {
            steps {
                script {
                    
                    def server = Artifactory.server ARTIFACTORY_SERVER
                    
                    def downloadSpec =readFile '/var/lib/jenkins/workspace/jfrog-jenkins/target/JPetStore.war'
                    def uploadSpec =readFile 'https://dincric.jfrog.io/artifactory/artifactory-build-info/'
                    
                    def buildInfo2 = server.upload spec: https://dincric.jfrog.io/artifactory/artifactory-build-info/
                        }
            }
        }




     

    }

}
