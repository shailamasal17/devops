pipeline {
    agent {
        docker {
            image 'docker:24.0'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                url: 'https://github.com/shailamasal17/devops.git'
            }
        }

        stage('Build & Deploy') {
            steps {
                sh '''
                docker build -t devops-app .
                docker stop devops-container || true
                docker rm devops-container || true
                docker run -d -p 3000:3000 --name devops-container devops-app
                '''
            }
        }
    }
}
