pipeline {
    agent any
	
    environment {
        PATH = "C:\\Users\\Gopal Sabale\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;${env.PATH}"
    }

    stages {
        stage('check the running container id') {
            steps {
                echo "checking the status of container"
                bat 'docker container ps -q'
            }
        }

        stage('creating the custom image from the running container') {
            steps {
                bat 'docker container commit $(docker container ps -q) custom_image'
            }
        }
    }
}
