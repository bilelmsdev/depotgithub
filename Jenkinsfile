pipeline {
    agent any
    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp-image .'
            }
        }
        stage('Clean Containers and Images') {
            steps {
                sh '''
                docker stop myapp 2>/dev/null || true
                docker rm myapp 2>/dev/null || true
                docker rmi myapp-image 2>/dev/null || true
                '''
            }
        }
        stage('Deploy Application') {
            steps {
                sh '''
                docker build -t myapp-image .
                docker run -d --name myapp -p 80:80 myapp-image
                '''
            }
        }
    }
}
