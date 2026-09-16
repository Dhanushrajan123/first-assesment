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

        stage('Run Container') {
            steps {
                sh '''
                    docker stop dhanush-container || true
                    docker rm dhanush-container || true

                    docker run -d \
                    --name dhanush-container \
                    -p 3000:80 \
                    dhanush-devops-app:latest
                '''
            }
        }
    }
}
