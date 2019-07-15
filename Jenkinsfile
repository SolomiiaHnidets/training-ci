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
    stage('Run app') {
      steps {
        dir(path: 'flask-app') {
          sh '''docker-compose down;
docker-compose rm -sf'''
        }

      }
    }
  }
}