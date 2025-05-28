pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "Code already checked out by Jenkins SCM"
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("vizzbob/sampleapp1:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'echo "Running tests..."'
                    }
                }
            }
        }

        stage('Push Docker Image') {
            when {
                branch 'master'
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
