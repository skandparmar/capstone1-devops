pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image"
                sh 'docker build -t capstone1-webapp:latest .'
            }
        }
    }

    post {
        success {
            script {
                echo "Build successful. Triggering Test job."
                build job: 'capstone1-test'

                if (env.BRANCH_NAME == 'master') {
                    echo "Master branch detected. Triggering Prod job."
                    build job: 'capstone1-prod'
                } else {
                    echo "Develop branch detected. Skipping Prod."
                }
            }
        }
    }
}
