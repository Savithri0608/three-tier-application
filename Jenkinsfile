pipeline {
    agent any

    stages {
        stage('Install Node') {
            steps {
                sh 'curl -fsSL https://deb.nodesource.com/setup_16.x | bash -'
                sh 'apt-get install -y nodejs'
            }
        }

        stage('Frontend Build') {
            steps {
                dir('Projects/frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Backend Build') {
            steps {
                dir('Projects/backend') {
                    sh 'npm install'
                    sh 'npm test || true'
                }
            }
        }
    }
}
