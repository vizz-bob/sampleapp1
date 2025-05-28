pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Use your actual repo URL here
                git 'https://github.com/vizz-bob/sampleapp1.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Replace your Docker Hub username and app name
                    dockerImage = docker.build("vizzbob/sampleapp1:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    dockerImage.inside {
                        // Replace with your real test command
                        sh 'echo Running tests...'
                    }
                }
            }
        }

        stage('Push Docker Image') {
            when {
                branch 'master' // or 'main' if that's your default branch
            }
            steps {
                withDockerRegistry(credentialsId: 'dockerhub-credentials', url: '') {
                    script {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
