pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t iramakhtar/duo-jenk:latest -t iramakhtar/duo-jenk:v${BUILD_NUMBER} .
                '''
            }
        }
        stage('Push') {
            steps {
                sh '''
                docker push iramakhtar/duo-jenk:latest
                docker push iramakhtar/duo-jenk:v${BUILD_NUMBER}
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh'''
                kubectl apply -f .
                kubectl set image deployment/flask-deployment flask-container=iramakhtar/duo-jenk:v${BUILD_NUMBER}
                '''
            }
        }
    }
}
