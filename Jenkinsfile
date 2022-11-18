pipeline {
  agent {
    docker {
      image 'node:lts-buster-slim'
      args '-p 3000:3000 -v /var/jenkins_home:/var/jenkins_home -w /var/jenkins_home'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Deliver') {
      steps {
        sh 'export NODE_OPTIONS=--openssl-legacy-provider && ./jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

  }
  environment {
    CI = 'true'
    npm_config_cache = 'npm-cache'
  }
}