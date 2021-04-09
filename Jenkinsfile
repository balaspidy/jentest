pipeline {
agent any
stages {
stage('Checkout Source') {
      steps {
        git 'https://github.com/balaspidy/jentest.git'
      }
    }
 stage('Apply Kubernetes files') {
    withKubeConfig([credentialsId: 'kubeid1', serverUrl: 'https://10.128.0.7:6443']) {
      sh 'kubectl apply -f '
    }
  }

    }
    }
