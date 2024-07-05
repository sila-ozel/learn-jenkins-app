pipeline {
    agent {
        docker {
            image 'node:slim'
            reuseNode true
        }
    }
    stages {
        stage('Verify') {
            steps {
                echo 'Verifying npm version'
                sh 'node --version && npm --version'
            }
        }
        stage('Build') {
            steps {
                echo 'Installing dependencies'
                sh 'npm ci'
                sh 'ls -la'
                sh 'npm run build'
                sh 'ls -la'
            }
        }
        stage('Test') {
            sh 'test ./build/index.html'
            sh 'npm test'
        }
    }
}