pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'virendrakr9/nodeapp' // Replace with your Docker Hub username
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Virendra-94/2_Jenkins_Pipeline_Setup' // Change to your repo
            }
        }
        
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }
        
        stage('Push Docker Image to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    bat """
                        echo %PASSWORD% | docker login -u %USERNAME% --password-stdin
                        docker push %DOCKER_IMAGE%
                    """
                }
            }
        }
    }
}
