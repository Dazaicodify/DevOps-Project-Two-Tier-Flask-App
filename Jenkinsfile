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
                // Stop old containers
                sh 'docker compose down || true'
                // Build and start new containers
                sh 'docker compose up -d --build'
            }
        }
        
        stage('Verify') {
            steps {
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
