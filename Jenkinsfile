pipeline {

  environment {
    registry = "localhost:5000/justme/mydocker"
    dockerImage = "felipenascimento26/user-service:0.0.1"
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
