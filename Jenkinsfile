pipeline {
    agent any
stages {

    stage('Docker Build') {
    	agent any
      steps {
      	sh 'docker build -t 301999322324.dkr.ecr.ap-south-1.amazonaws.com/cicd:latest .'
        
      }
    }
        stage('Logging into AWS ECR') {
 steps {
 withAWS(credentials: 'awscred', region: 'ap-south-1') {
script {
   sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 301999322324.dkr.ecr.ap-south-1.amazonaws.com'
   sh 'docker push 301999322324.dkr.ecr.ap-south-1.amazonaws.com/cicd:latest'
}

}
 }
    }
  stage('Apply Kubernetes files') {
      steps {
 withAWS(credentials: 'awscred', region: 'ap-south-1') {
                  script {
                    def tag = 22.7-${env.BUILD_NUMBER}
                    sh ' echo $tag '
                    sh ('aws eks update-kubeconfig --name eksdemo1 --region ap-south-1')
                   // sh  'sed -i 's/latest/$tag/p' appdeploy.yaml'
                    sh "/tmp/kubectl apply -f appdeploy.yaml"
                }
                }
    
    }
  }
}
}
