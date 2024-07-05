pipeline {
    agent {
        docker {
            image 'node:slim'
            args "-p 3000:3000"
        }
    }
    stages {
        stage('Verify') {
            steps {
                echo 'Verifying npm version'
                sh 'npm --version'
            }
        }
        stage('Build') {
            steps {
                echo 'Installing dependencies'
                sh 'npm install'
            }
        }
        stage('Run') {
            steps {
                echo 'Starting the development server'
                sh 'npm start'
            }
        }
    }
}