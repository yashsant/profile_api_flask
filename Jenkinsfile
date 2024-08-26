pipeline {
    agent {label 'jenkins-docker'}
    options{
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }
    environment{
        
        registry = "yashspam/profile-api"
        registryCredential = 'dockerhubId'        
    }
    stages{
        steps {
            sh 'cd app'
        }
    }
    
    stages{
       stage('Build') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
       stage('Deploy') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
}
}
