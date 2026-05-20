pipeline {
    agent any
    stages {
        stage('Verify Code') {
            steps {
                sh 'ls -la'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp .'
            }
        }
        stage('Stop Old Container') {
            steps {
                sh 'docker stop mycontainer || true'
                sh 'docker rm mycontainer || true'
            }
        }
        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 80:8080 --name mycontainer myapp'
            }
        }
    }
}

