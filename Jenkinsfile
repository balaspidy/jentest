pipeline {
agent any
stages {
stage('Checkout Source') {
      steps {
        git 'https://github.com/balaspidy/jentest.git'
      }
    }
stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "frontend.yaml", kubeconfigId: "kubeid1")
        }
      }
    }
    }
    }
