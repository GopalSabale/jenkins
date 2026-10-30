pipeline {

    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }

    environment {
        PATH = "C:\\Users\\Gopal Sabale\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;${env.PATH}"
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
                    docker container commit %%i custom_image_1
                )
                '''
            }
        }
    }
}