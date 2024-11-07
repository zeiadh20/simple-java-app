// pipeline{
//     agent{
//         label 'aws-agent'
//     }
//     stages{
//         stage('build'){
//             steps{
//                 script{
//                     sh 'docker build -t java-app .'
//                 }
//             }
//         }

//         stage('push'){
//             steps{
//                 script{
//                     withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'Password', usernameVariable: 'Username')]) {
//                     sh 'docker login --username $Username --password $Password'
//                     sh 'docker tag java-app $Username/java-app'
//                     sh 'docker push $Username/java-app'
//                     }
//                 }
//             }
//         }

//         stage('deploy'){
//             steps{
//                 script{
//                     withAWS(credentials: 'aws-cli', region: 'us-east-2') {
//                     sh 'aws eks update-kubeconfig --region us-east-2 --name eks'
//                     sh 'kubectl apply -f ./k8s/deployment.yaml'
//                     }
//                 }
//             }
//         }
//     }
// }




// scripted pipeline

pipeline {
    agent {
      label 'aws-agent'
    }

    stages {
        stage('build') {
            steps {
              sh 'mvn clean package'
            }
        }
        
        stage('test') {
            steps {
                sh 'echo "test in progress"'
            }
        }
    }

    post {
        success {
            slackSend(
                channel: '#jenkins', 
                message: "Build Success - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", 
                teamDomain: 'dolfined', 
                tokenCredentialId: 'slack-notification'
            )
        }
        failure {
            slackSend(
                channel: '#jenkins', 
                message: "Build Failure - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", 
                teamDomain: 'dolfined', 
                tokenCredentialId: 'slack-notification'
            )
        }
    }
}


// pipeline{
//   agent any
//   stages{
//     stage('build'){
//       steps{
//         script{
//           echo "build in progress"
//         }
//       }
//     }
//   }
// }






