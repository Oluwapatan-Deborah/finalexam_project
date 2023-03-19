pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = "us-east-1"
    }
  
    stages {
        stage("Create Prometheus") {
            steps {
                dir('prometheus') {
                    sh "aws eks --region us-east-1 update-kubeconfig --name exam"
                    sh "terraform init"
                    sh "terraform apply -auto-approve"
                }
            }
        }
      
        stage("Create Nginx-controller") {
            steps {
                dir('nginx-controller') {
                    sh "terraform init"
                    sh "terraform apply -auto-approve"
                }
            }
        }
      
        stage("Deploy Voting App to EKS") {
            steps {
                dir('voting-app') {
                    sh "terraform init"
                    sh "terraform apply -auto-approve"
                }
            }
        }
      
        stage("Deploy Microservice to EKS") {
            steps {
                dir('sock-shop') {
                    sh "terraform init"
                    sh "terraform apply -auto-approve"
                }
            }
        }
      
        stage("Deploy Ingress rule to EKS") {
            steps {
                dir('ingress-rule') {
                    sh "terraform init"
                    sh "terraform apply -auto-approve"
                }
            }
        }
    }
}
