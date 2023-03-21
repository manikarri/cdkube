pipeline {
    agent any
stages {
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
