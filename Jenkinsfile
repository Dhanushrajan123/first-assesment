pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t dhanush-devops-app:latest .'
            }
        }

        stage('Test Docker Image') {
            steps {
                sh 'docker images dhanush-devops-app:latest'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker stop dhanush-container || true
                    docker rm dhanush-container || true

                    docker run -d \
                        --name dhanush-container \
                        -p 8080:80 \
                        dhanush-devops-app:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
