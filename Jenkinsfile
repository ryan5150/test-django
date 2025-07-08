pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/ryan5150/test-django'
      }
    }
    stage('Login to ECR') {
      steps {
        withAWS(region: 'us-east-2', credentials: 'aws-creds') {
          powershell '''
            $password = aws ecr get-login-password --region us-east-2
            docker login --username AWS --password $password 067632295443.dkr.ecr.us-east-2.amazonaws.com
          '''
        }
      }
    }
    stage('Build docker image') {
      steps {
        powershell '''
          docker build -t test2:rturner .
          docker tag test2:rturner 067632295443.dkr.ecr.us-east-2.amazonaws.com/test2:rturner
        '''
      }
    }
    stage('Pushing image to ECR') {
      steps {
        powershell '''
          docker push 067632295443.dkr.ecr.us-east-2.amazonaws.com/test2:rturner
        '''
      }
    }
  } 
}   
