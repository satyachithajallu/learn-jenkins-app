pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            steps {
                sh 'echo "Test stage"'
                sh 'test -f ./build/index.html && echo "File exists" || echo "File doesnot exist"'
                sh 'npm test'
            }
        }
    }
}