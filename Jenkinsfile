pipeline {

agent any 
 
  stages{

         stage('Git chceckout'){

           steps{
                             git branch: 'main', url: 'https://github.com/PoudelAmrit123/ci-cd-pipeline.git'
                }
                             }
        stage('Unit Test'){
            steps{
                sh 'mvn test'
            }
        }

        stage('Integrated testing'){

            steps{
                sh 'mvn verify -DskipUnitTests'
            }
        }

        stage('Maven Build'){

            steps{
                sh 'mvn clean install'
            }
        }

        stage('Static Code Analysis'){

            steps{
                script{
                        withSonarQubeEnv(credentialsId: 'sonar-api') {
                            sh 'mvn clean package sonar:sonar'
                             }
                     }
            }
        }

      //  stage('Quality Gate status'){
//      steps{

         //       script{
          //          waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
          //      }
          //   }


       // }

       stage('Upload jar File To nexus'){

         steps{
            script{
                nexusArtifactUploader artifacts:
                 [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']],
                  credentialsId: 'nexus-auth', 
                  groupId: 'com.example', 
                  nexusUrl: 'https://www.howtoforge.com/how-to-install-and-configure-nexus-repository-manager-on-ubuntu-20-04/', 
                  nexusVersion: 'nexus3', 
                  protocol: 'http', 
                  repository: 'demoapp-release', 
                  version: '1.0.0'
            }

         }

       }


  }


}