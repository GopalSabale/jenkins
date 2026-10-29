pipeline {
    agent any

    stages {
        stage('check the running container id') {
            steps {
                echo "checking the status of container"
                sh 'docker container ps -q'
            }
        }

        stage('creating the custom image from the running container') {
            steps {
                sh 'docker container commit $(docker container ps -q) custom_image'
            }
        }
    }
}