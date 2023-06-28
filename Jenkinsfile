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

        stage('Quality Gate status'){
             steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                }
             }


        }


  }


}