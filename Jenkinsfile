pipeline {
     agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:22.14.0-alpine'
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
                    image 'node:22.14.0-alpine'
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
                withCredentials([usernamePassword(credentialsId: 'my-aws-s3', passwordVariable: 'DtvgZJ4YSTdwehBFv2pJp0g6tIOHl5qtNwtUROv', usernameVariable: 'AKIAT7PQ33CV5FYZYSYM')]) {
                    sh '''
                        aws --version
                        aws s3 ls
                    '''
                }
                
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