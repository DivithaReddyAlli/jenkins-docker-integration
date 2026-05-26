pipeline {
    agent any
    environment {
        IMAGE_NAME = "divithaalli/myapp"
    }
    stages {
        stage('Clone Code') {
            steps {
                sh 'ls -la'
            }
        }
        stage('Build Image') {
            steps {
                sh '/usr/bin/docker build -t $IMAGE_NAME:latest .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | /usr/bin/docker login -u $USER --password-stdin'
                    sh '/usr/bin/docker push $IMAGE_NAME:latest'
                }
            }
        }
        stage('Deploy to EC2 via SSH') {
            steps {
                sh '''
                ssh -o StrictHostKeyChecking=no ubuntu@localhost << 'EOF'
                sudo /usr/bin/docker pull divithaalli/myapp:latest
                sudo /usr/bin/docker stop myapp || true
                sudo /usr/bin/docker rm myapp || true
                sudo /usr/bin/docker run -d --restart always -p 80:3000 --name myapp divithaalli/myapp:latest
                EOF
                '''
            }
        }
    }
}
