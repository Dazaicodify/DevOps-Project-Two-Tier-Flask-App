pipeline {
    agent any
    
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/Dazaicodify/DevOps-Project-Two-Tier-Flask-App.git'
            }
        }
        
        stage('Deploy with Docker Compose') {
            steps {
                echo 'Stopping old containers...'
                sh 'docker-compose down || true'
                
                echo 'Building and starting containers...'
                sh 'docker-compose up -d --build'
            }
        }
        
        stage('Verify') {
            steps {
                echo 'Checking running containers...'
                sh 'docker ps'
            }
        }
    }
    
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
