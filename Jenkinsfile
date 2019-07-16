pipeline {
  agent {
    node {
      label 'instance-1'
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
    stage('Run tests') {
      steps {
        dir(path: 'flask-app') {
          sh '''docker-compose down
docker-compose build flask-app
docker-compose run flask-app pytest -v --junit-xml=/var/opt/junit-report/report.xml
docker-compose down'''
        }

      }
    }
    stage('Archive JUnit-formatted test results') {
      steps {
        junit(allowEmptyResults: true, testResults: 'flask-app/junit-report/report.xml')
        sh 'sudo rm -rf flask-app/junit-report'
      }
    }
  }
}