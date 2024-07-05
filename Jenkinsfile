pipeline {
    agent {
        docker {
            image 'node:slim'
            reuseNode true
        }
    }
    stages {
        // disabled verify stage for a better performance
        /* stage('Verify') {
            steps {
                echo 'Verifying npm version'
                sh 'node --version && npm --version'
            }
        } */
        /* stage('Build') {
            steps {
                echo 'Installing dependencies'
                sh 'npm ci'
                sh 'ls -la'
                sh 'npm run build'
                sh 'ls -la'
            }
        } */
        stage('Test') {
            steps {
                sh 'test -f ./build/index.html'
                sh 'npm test && test -f test-results/junit.xml'
            }
        }
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }

}