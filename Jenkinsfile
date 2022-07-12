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
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u javatechie -p ${dockerhubpwd}'

        }
                   sh 'docker push javatechie/devops-integration'
                }
            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'kubepod')
                }
            }
        }
    }
}