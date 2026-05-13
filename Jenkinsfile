pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                sh '''
                # Stop and force remove old container if it already exists
                docker rm -f jenkinscontainer || true
                
                # Build the new image using your Day 22 file blueprint
                docker build -t myjenkinsapp .
                
                # Launch the container onto port 8095
                docker run -d -p 8095:80 --name jenkinscontainer myjenkinsapp
                '''
            }
        }
    }
}
