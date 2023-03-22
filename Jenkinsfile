pipeline {
    agent any
stages {
    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t 301999322324.dkr.ecr.ap-south-1.amazonaws.com/cicd:latest .'
        sh 'docker push 301999322324.dkr.ecr.ap-south-1.amazonaws.com/cicd:latest'
      }
    }
  stage('Apply Kubernetes files') {
      steps {
 withAWS(credentials: 'awscred', region: 'ap-south-1') {
                  script {
                    sh ('aws eks update-kubeconfig --name eksdemo1 --region ap-south-1')
                    sh "/tmp/kubectl apply -f appdeploy.yaml"
                }
                }
    
    }
  }
}
}
