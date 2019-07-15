pipeline {
  agent {
    node {
      label 'master'
    }

  }
  stages {
    stage('Echo Some Text') {
      steps {
        sh 'echo "Some text 123"'
        sh 'echo "hello 1"'
      }
    }
    stage('Git Checkout') {
      steps {
        git(url: 'https://github.com/SolomiiaHnidets/training-ci', branch: 'master', credentialsId: '6217ceda-8f89-44e7-a3e3-a09a1981f91e')
      }
    }
    stage('Run App') {
      steps {
        dir(path: 'flask-app') {
          sh 'docker-compose up -d --build'
        }

      }
    }
  }
}