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
                sh 'docker build -t divithaalli/myapp:latest .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push divithaalli/myapp:latest'
                }
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
                sh 'docker run -d -p 80:8080 --name mycontainer divithaalli/myapp:latest'
            }
        }
    }
}

