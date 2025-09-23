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
                    npm cache clean --force
                    timeout 300 npm ci --verbose
                    ls -la
                    node --version
                    npm  --version
                    npm ci
                    npm run build
                    ls -la
                
                '''
            }
        }
        stage('Test') {

            steps {
              sh '''
                test -f build/index.html



               '''
            }                
        }
    }
}
