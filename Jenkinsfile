pipeline {
    
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:22-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    # npm install
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:22-alpine'
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
        
        stage('Deploy') {
            agent {
                docker {
                    image 'amazon/aws-cli'
                    reuseNode true
                    args '--entrypoint=""'
                }
            }
            steps {
                sh '''
                    aws --version
                    aws s3 ls
                '''
            }
        }
            
    }
    
}

/*
post {
        always {
            echo 'Pipeline completed!'
        }
        success {
            echo '✅ Success!'
        }
        failure {
            echo '❌ Failed! Check logs.'
        }
    }
*/