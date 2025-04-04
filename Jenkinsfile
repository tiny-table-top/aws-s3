pipeline {
    agent {
        docker {
            image 'node:22.14.0'         // Official Node.js image
            args '--isolation=hyperv'    // Required for Windows containers
            label 'windows'              // Run on a Windows agent
        }
    }
    stages {
        stage('Check Node & NPM') {
            steps {
                bat 'node --version'     // Use `bat` for Windows CMD
                bat 'npm --version'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }
        stage('Build App') {
            steps {
                bat 'npm run build'
            }
        }
    }
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
}