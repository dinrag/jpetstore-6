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
           
           
                withCredentials([usernamePassword(credentialsId: 'jfrog', passwordVariable: 'JfrogPass', usernameVariable: 'JfrogUser')]) {
                   sh ''' 
                wget --http-user=$JfrogUser --http-password=$JfrogPass  https://sakthishivani.jfrog.io/artifactory/libs-snapshot-local/org/mybatis/jpetstore/6.0.3-SNAPSHOT/jpetstore-6.0.3-SNAPSHOT.war
                cp  jpetstore-6.0.3-SNAPSHOT.war /home/dineshreddy99077/noida/apache-tomcat-7.0.103/webapps/
                '''
           
           }
        }
               
        }



     

    }

}
