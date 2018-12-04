pipeline {
         agent any

         environment {
            PATH = "$PATH:/usr/maven/bin"
          }

         stages {
         stage('Checkout external proj') {
              steps {
                git branch: 'master',
                //  credentialsId: 'my_cred_id', 'Get DOwn it from /var/lib/jenkins/credentials.xml'
                url: 'https://github.com/avinashsi/javaproject.git'

                  }
                }
          stage('Compile_Maven_Code') {
              steps {
                mvn clean package,
                }
             }

// This is where Things Should go TO nexus Commenting out due to memory issues ///////

//        Satge ('Nexus Artifact_Upload'){
//             steps {
//                nexusArtifactUploader {
//                nexusVersion('nexus3')
//                protocol('http')
//                nexusUrl('localhost:8081/nexus')
//                groupId('sp.sd')
//                version('3.14')
//                repository('maven_rmg_repo')
//                Got from /var/lib/jenkins/credentials.xml
//                credentialsId('44620c50-1589-4617-a677-7563985e46e1')
//                artifact {
//                    artifactId('maven_rmg_repo')
//                    type('war')
//                    classifier('debug')
//                    file('trucks.war')
//                  }
//                }
//              }
//


// This is where Things Should Downloaded from Nexus ///////
//  Nexus Is down due to memory issue ////////////////////
//COPYING FILE INSTEAD from Local directory
//        Satge ('Download articats from Nexus'){
//             steps {
//               wget http://nexus_url:8081/repo/trucks.jar
//                }
//              }
//

//////Coping directory jar file in local file system //////////////////////////////

        Satge ('Copying Files Locally'){
             steps {
               cp /var/lib/jenkins/workspace/mvnTest/target/trucks.war /home/vagrant/files/app_data/application1/
                }
              }

        Stage ('Get The DockerFile'){
            steps{
              git branch: 'master',
              //  credentialsId: 'my_cred_id', 'Get DOwn it from /var/lib/jenkins/credentials.xml'
              url: 'https://github.com/avinashsi/dockerfile.git'
                  }
                }
        Stage ('Get The DockerFile'){
            steps{
                git branch: 'master',
               //  credentialsId: 'my_cred_id', 'Get DOwn it from /var/lib/jenkins/credentials.xml'
                url: 'https://github.com/avinashsi/dockerfile.git'
                  }
                }

        //THis Jar should come from Nexus.

        Stage ('Add the war file){
              steps{
              cat >> /dockerfile/Tomcat8_Dockerfile/Dockerfile <<EOL
              ADD /home/vagrant/files/app_data/application1/trucks.war /home/tomcat/webapps/
              EOL
                  }
              }
        // Build the Docker Image

        Stage ('Build The Image'){
              steps{
               docker build -t  tomcat":$BUILD_NUMBER" /dockerfile/Tomcat8_Dockerfile/.
              }
            }


          }
}
