pipeline {
  
  environment {
    registry = "ajjaiii/myweb"
    registryCredential = 'dockerhub'
  }
  
  agent any
  stages {

    stage('Checkout update repo') {
      steps {
        git 'https://github.com/ajjaiii/playjenkins.git'
      }
    }

  stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }  
  
  stage('Push Docker Image') {
  steps{
    script {
      docker.withRegistry( '', registryCredential ) {
        dockerImage.push()
        }
      }
    }
  }
  
  
  stage('Deploy App to kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }
  
  stage('Remove Unused docker image') {
     steps{
       sh "docker rmi $registry:$BUILD_NUMBER"
       }
     }  
      
  }
}
