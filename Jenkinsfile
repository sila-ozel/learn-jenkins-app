pipeline {
    agent any
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
            agent {
                docker {
                    image 'node:slim'
                    reuseNode true
                }
            }
            steps {
                sh 'test -f ./build/index.html'
                sh 'npm test && test -f test-results/junit.xml'
            }
        }
        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.45.1-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                npm install serve
                node_modules/.bin/serve -s build &
                sleep 10
                npx playwright test
                '''
            }
        }
    }
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }

}