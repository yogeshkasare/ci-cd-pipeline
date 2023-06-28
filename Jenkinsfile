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


  }


}