pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
    }

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t simple-app:1.0 .'
            }
        }

        stage('Tag Image') {
            steps {
                sh 'docker tag simple-app:1.0 oriyahazan/simple-app:1.0'
            }
        }

        stage('Push Image') {
            steps {
                sh '''
                echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
                docker push oriyahazan/simple-app:1.0
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh 'ansible-playbook deploy-playbook.yml'
            }
        }
    }
}
