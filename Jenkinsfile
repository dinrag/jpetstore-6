pipeline {

    agent any

    stages {

        stage ('Clone') {

            steps {

                git branch: 'master', url: "https://github.com/dinrag/jpetstore-6.git"

            }

        }
                     
        stage ('package') {

            steps {


                    sh './mvnw clean package'

            }

         }
        stage ('sonar') {

            steps {


                    sh '/opt/apps/devops/sonar-scanner-4.2.0.1873-linux/bin/sonar-scanner'

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

        
        stage ('deploy') {
            
           
            steps {

              //sh 'rm -rf /home/dineshreddy99077/noida/apache-tomcat-7.0.103/webapps/JPetStore'
              //sh 'rm -f /home/dineshreddy99077/noida/apache-tomcat-7.0.103/webapps/JPetStore.war' 
                
              sh 'cp target/JPetStore.war https://dincric.jfrog.io/ui/repos/tree/General/artifactory-build-info'

            }
            }
        
       



     

    }

}
