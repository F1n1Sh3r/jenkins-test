pipeline {

  environment {
    registry = "localhost:5000/justme/myweb"
    dockerImage = ""
  }

    agent { label 'user-service-app'}

  stages {

    stage('Checkout Source') {
      steps {
        git 'git@github.com:F1n1Sh3r/jenkins-test.git'
      }
    }

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
