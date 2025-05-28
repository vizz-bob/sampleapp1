pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "vizzbob/sampleapp1:4"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo "Building the app with Maven"
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo "Building Docker image"
                sh "docker build -t ${DOCKER_IMAGE} ."
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-credentials-id') {
                        docker.image(DOCKER_IMAGE).push()
                    }
                    pipeline {
    agent any
    tools {
        maven 'Maven 3.8.6' // The name you configured in Global Tool Configuration
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        // rest of pipeline
    }
}

                }
            }
        }
    }
}
