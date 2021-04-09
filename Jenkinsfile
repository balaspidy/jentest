pipeline {
agent any
stages {
stage('Checkout Source') {
      steps {
        git 'https://github.com/balaspidy/Docker-Project.git'
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
