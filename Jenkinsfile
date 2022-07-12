pipeline {
    agent any
    tools{
        maven '3.8.6'
    }
    stages{
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t felipenascimento26/user-service:0.0.1'
                }
            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'user-service.yaml',kubeconfigId: 'kubernetes')
                }
            }
        }
    }
}