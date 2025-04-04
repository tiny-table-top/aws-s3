pipeline {
  agent {
    docker {
      image 'node:22.14.0'  // Uses official Node.js image
    }
  }
    
  stages {
    stage('Build') {
      
      steps {
        sh 'npm install'
      }
    }

  }

}


/*
stage('Test') {
      steps {
        sh 'npm test'
      }
    }
*/