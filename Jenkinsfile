pipeline {
environment {
    namespace1 = "prod"
    namespace2 = "dev"
  }
agent any
stages {
stage('Checkout Source') {
      steps {
        git 'https://github.com/balaspidy/jentest.git'
      }
    }
stage('Apply Kubernetes files') {
  when { branch "master" }
    steps {
    withKubeConfig([credentialsId: 'kubeid', serverUrl: 'https://10.128.0.7:6443']) {
    sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
    sh 'chmod u+x ./kubectl' 
    sh 'cat frontend.yaml | sed "s/{{namespace}}/$namespace1/g" | `pwd`/kubectl apply -f -'
    }
    }
  }

    }
    }
