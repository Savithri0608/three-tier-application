pipeline {
    agent {
        docker {
            image 'node:16'
            args '-u root:root'
        }
    }

    environment {
        FRONTEND = "Dockerfile-Projects/frontend"
        BACKEND  = "Dockerfile-Projects/backend"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Savithri0608/three-tier-application.git'
            }
        }

        stage('Install Frontend') {
            steps {
                dir("${DOCKERFILE-PROJECTS/FRONTEND}") {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Install Backend') {
            steps {
                dir("${DOCKERFILE-PROJECTS/BACKEND}") {
                    sh 'npm install'
                    sh 'npm test || true'
                }
            }
        }

        stage('Skip Docker Build') {
            steps {
                echo "Docker build skipped because images already built."
            }
        }
    }
}
