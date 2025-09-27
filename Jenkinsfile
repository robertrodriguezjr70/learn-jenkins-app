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
                timeout(time: 5, unit: 'MINUTES') {
                    sh '''
                        npm cache clean --force
                        npm ci --verbose
                        ls -la
                        node --version
                        npm --version
                        npm run build
                        ls -la
                    '''
                }
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
    }
}
