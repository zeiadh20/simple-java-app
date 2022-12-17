pipeline{

  agent{
      label 'aws-agent'
  }

  stages{

    stage('build'){
      steps{
        script{
          sh 'mvn clean package'
        }
      }
    }

    stage('test'){
      steps{
        script{
          echo  "test in progress"
        }
      }
    }

  }

post {
  success {
   slackSend channel: '#jenkins-ci', message: "Build success - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'myproject-vx43962', tokenCredentialId: 'slack-notification'
  }
  failure {
   slackSend channel: '#jenkins-ci', message: "Build failed - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", teamDomain: 'myproject-vx43962', tokenCredentialId: 'slack-notification'
  }
}

}
