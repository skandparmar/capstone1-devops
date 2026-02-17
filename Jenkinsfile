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

                echo "Git Branch: ${env.GIT_BRANCH}"

                if (env.GIT_BRANCH.contains("master")) {
                    echo "Master branch detected. Triggering Prod job."
                    build job: 'capstone1-prod'
                } else {
                    echo "Develop branch detected. Skipping Prod."
                }
            }
        }
    }
}
