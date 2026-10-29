pipeline {
    agent any
    stages {
        stage('check the running container id') {
            echo "checking the status of container"
            'docker container ps -q'
        }
        stage('creating the custom image from the running container') {
            'docker container commit $(docker container ps -q) custom_image' 
       }
    }
}