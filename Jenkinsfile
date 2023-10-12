pipeline {
    agent any

    environment {
        QUAY_CREDS = credentials('test-quay')
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t quay.io/csye7125organization/test:latest .'
            }
        }

        stage('Login') {
            steps {
                sh 'echo $QUAY_CREDS_PSW | docker login quay.io -u $QUAY_CREDS_USR --password-stdin'
            }
        }

        stage('PUSH') {
            steps {
                sh 'docker push quay.io/csye7125organization/test:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout quay.io'
        }
    }
}