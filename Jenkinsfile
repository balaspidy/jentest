pipeline {
environment {
    namespace1 = "prod"
    namespace2 = "dev"
    port1 = "32333"
    port2 = "32334"
    registry1 = "spidybala/nginx-prd"
    registry2 = "spidybala/nginx-dev"
    registryCredential = 'dockerhub'
    image1 = "spidybala\\/nginx-prd\\" + ":$BUILD_NUMBER"
    image2 = "spidybala\\/nginx-dev\\" + ":$BUILD_NUMBER"
  }
agent any
stages {
    
stage('Docker build for Prod') {
 when { branch "master" }
    steps {
      script {
          dockerImage = ''
          dockerImage = docker.build registry1 + ":$BUILD_NUMBER"
         
      }
    }
} 
    
stage('Docker build for Dev') {
 when { 
     expression {
            return env.BRANCH_NAME != 'master';
 }
 }
    steps {
      script {
          dockerImage = ''
          dockerImage = docker.build registry2 + ":$BUILD_NUMBER"
         
      }
    }
}
    
 stage('Push image') {
     steps{
         script{
        withDockerRegistry(credentialsId: "dockerhub", url: "") {
        dockerImage.push()
        }
 }
     }
 }
stage('Apply Kubernetes files in Prod') {


  when { branch "master" }
    steps {
    git 'https://github.com/balaspidy/jentest.git'
    withKubeConfig([credentialsId: 'kubeid', serverUrl: 'https://10.128.0.7:6443']) {
    sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
    sh 'chmod u+x ./kubectl'
     sh 'image1= echo "spidybala\\/nginx-prd\\:$BUILD_NUMBER"'
    sh 'cat frontend.yaml | sed "s/{{namespace}}/$namespace1/g"| sed "s/{{port}}/$port2/g" |sed "s/{{dockerimage}}/$image1/g"| `pwd`/kubectl apply -f -'
    }
    }
  }
 
  stage('Apply Kubernetes files in Dev') {
  when { 
         expression {
            return env.BRANCH_NAME != 'master';
        }
  }
    steps {
    git branch: 'test', url: 'https://github.com/balaspidy/jentest.git'
    withKubeConfig([credentialsId: 'kubeid', serverUrl: 'https://10.128.0.7:6443']) {
    sh 'curl -LO "https://storage.googleapis.com/kubernetes-release/release/v1.20.5/bin/linux/amd64/kubectl"'  
    sh 'chmod u+x ./kubectl'
    sh 'image2= echo "spidybala\\/nginx-dev\\:$BUILD_NUMBER"'
    sh 'cat frontend.yaml | sed "s/{{namespace}}/$namespace2/g"| sed "s/{{port}}/$port1/g" |sed "s/{{dockerimage}}/$image2/g"| `pwd`/kubectl apply -f -'
    }
    }
  }
}
}

