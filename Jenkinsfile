pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDS = credentials('dockerhub-creds')
    }

    stages {

        stage('Checkout') {
    steps {
        git branch: 'main',
            credentialsId: 'github-creds',
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

        stage('Docker Login') {
            steps {
                sh "echo ${DOCKER_HUB_CREDS_PSW} | docker login -u ${DOCKER_HUB_CREDS_USR} --password-stdin"
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t savithri06/frontend:latest Dockerfile-Projects/frontend'
                sh 'docker build -t savithri06/backend:latest Dockerfile-Projects/backend'
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push savithri06/frontend:latest'
                sh 'docker push savithri06/backend:latest'
            }
        }
    }
}
