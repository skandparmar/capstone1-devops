pipeline {
    agent any

    environment {
        IMAGE_NAME = "capstone1-webapp"
    }

    stages {

        stage('Build') {
            steps {
                echo "Building Docker Image"
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Test') {
            steps {
                echo "Testing Application"
                sh "docker run --rm ${IMAGE_NAME}:latest ls /var/www/html"
            }
        }

        stage('Prod') {
            when {
                branch 'master'
            }
            steps {
                echo "Deploying to Production"
                sh '''
                docker rm -f capstone1-prod || true
                docker run -d --name capstone1-prod -p 80:80 capstone1-webapp:latest
                '''
            }
        }
    }
}
