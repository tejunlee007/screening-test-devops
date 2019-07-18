pipeline {
  agent {
    docker {
      image 'python:3.6.5'
    }
  }
  stages {
    stage('build') {
      steps {
        sh 'pip install --trusted-host pypi.python.org -r ./backend/requirements.txt'
      }
    }
    stage('test') {
      environment {
        CI = 'true'
      }
      steps {
        sh 'pytest ./backend'
      }
    }
    stage('push') {
      agent none
      steps {
        sh  './push.sh'
      }
    }
  }
  environment {
    PYTHONUNBUFFERED = '1'
    PATH = '$PATH:/backend'
    PYTHONPATH = '$PYTHONPATH:/:/backend'

    registry = 'tejunlee007/screening-test-backend'
    registryCredential = 'dockerhub'
    backendImage = ''
  }
}
