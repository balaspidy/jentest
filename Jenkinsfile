pipeline {
agent any
stages {
stage('Checkout Source') {
      steps {
        git 'https://github.com/balaspidy/jentest.git'
      }
    }
 stage('Apply Kubernetes files') {
       STEPS{
             echo "$GIT_BRANCH"
  }

    }
    }
