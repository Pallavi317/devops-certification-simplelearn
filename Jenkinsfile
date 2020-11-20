pipeline {

  environment {
    registry = "pallavi173/devops-certification-simplilearn"
    registryCredential = 'Ericsson@173'
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Image') {
      steps{
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}

node {
    stage('Execute Image'){
        def customImage = docker.build("pallavi173/devops-certification-simplilearn:${env.BUILD_NUMBER}")
        customImage.inside {
            sh 'echo Hello'
        }
    }
}
