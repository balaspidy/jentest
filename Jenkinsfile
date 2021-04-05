pipeline {
agent any
stages {
stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "frontend.yaml", kubeconfigId: "kube.conf (kubeid)")
        }
      }
    }
    }
    }
