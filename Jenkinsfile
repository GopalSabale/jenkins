pipeline {

    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    environment {
        PATH = "C:\\Users\\Gopal Sabale\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;${env.PATH}"
        AWS_REGION = "ap-south-1"
        AWS_ACCOUNT_ID = "158909019760"
        ECR_REPO = "demo"
        ECR_URL = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
    }

    stages {

        stage('check the running container id') {
            steps {
                bat 'docker container ps -q'
            }
        }

        stage('creating custom image') {
            steps {
                bat '''
                for /f %%i in ('docker container ps -q') do (
                    docker container commit %%i custom_image_2
                )
                '''
            }
        }

        stage('login aws ECR') {
            steps {
                withCredenitials([
                    [
                        $class: 'AmazonWebServicesCredentialsBinding',
                        credentialsId: 'aws-creds'
                    ]

                ]){
                    bat '''
                    aws ecr get-login-password --region %AWS_REGION% | docker login --username AWS --password-stdin %ECR_URL%
                    '''
                }
            }
        }
        stage('tag docker image') {
            steps{
                '''
                bat docker tag custom_image_2:latest %ECR_URL%/%ECR_REPO%:v2
                '''
            }
        }
        stage('push docker image') {
            steps {
                '''
                docker image push %ECR_URL%/%ECR_REPO%:v1 
                '''
            }
        }
    }
}