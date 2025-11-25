pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Savithri0608/three-tier-application.git'
            }
        }

        stage('Install Frontend') {
            steps {
                dir('Dockerfile-Projects/frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Install Backend') {
            steps {
                dir('Dockerfile-Projects/backend') {
                    sh 'npm install'
                    sh 'npm test || true'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t savithri06/frontend:latest Dockerfile-Projects/frontend'
                sh 'docker build -t savithri06/backend:latest Dockerfile-Projects/backend'
            }
        }
    }
}
