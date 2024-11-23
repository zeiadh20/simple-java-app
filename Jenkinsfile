pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t java-app .'
                }
            }
        }

        stage('Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                        sh 'docker login --username $Username --password $Password'
                        sh 'docker tag java-app $Username/java-app'
                        sh 'docker push $Username/java-app'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    withAWS(credentials: 'aws-cli', region: 'us-east-1') {
                        sh 'aws eks update-kubeconfig --region us-east-1 --name eks'
                        sh 'kubectl apply -f ./k8s/deployment.yaml'
                    }
                }
            }
        }
    }
}
