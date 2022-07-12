pipeline {

  environment {
    registry = "felipenascimento26/user-service:0.0.1"
    registryCredential = 'dockerhub'
  }

    agent { label 'windows'}

  stages {

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "user-service.yaml", kubeconfigId: "default")
        }
      }
    }

  }

}
