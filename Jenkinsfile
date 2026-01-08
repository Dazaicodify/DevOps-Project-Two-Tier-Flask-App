pipeline {
    agent any
    
    environment {
        COMPOSE_PROJECT_NAME = 'flask-cicd'
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                echo '📥 Cloning repository from GitHub...'
                git branch: 'main', 
                    url: 'https://github.com/Dazaicodify/DevOps-Project-Two-Tier-Flask-App.git'
                echo '✅ Repository cloned successfully!'
            }
        }
        
        stage('Stop Old Containers') {
            steps {
                echo '🛑 Stopping old containers...'
                sh 'docker compose down || true'
                echo '✅ Old containers stopped!'
            }
        }
        
        stage('Build and Deploy') {
            steps {
                echo '🔨 Building images and starting containers...'
                sh 'docker compose up -d --build'
                echo '✅ Containers started successfully!'
            }
        }
        
        stage('Verify Deployment') {
            steps {
                echo '🔍 Verifying deployment...'
                sh 'docker compose ps'
                sh 'docker ps'
                echo '✅ Deployment verified!'
            }
        }
        
        stage('Health Check') {
            steps {
                echo '🏥 Running health check...'
                sh 'sleep 10'  // Wait for Flask to fully start
                sh 'curl -f http://localhost:5000 || exit 1'
                echo '✅ Application is responding!'
            }
        }
        
        stage('Clean Up Old Images') {
            steps {
                echo '🧹 Cleaning up old Docker images...'
                sh 'docker image prune -f || true'
                echo '✅ Cleanup complete!'
            }
        }
    }
    
    post {
        success {
            echo '🎉 Pipeline executed successfully!'
            echo '✅ Application deployed and running at http://YOUR_SERVER_IP:5000'
        }
        failure {
            echo '❌ Pipeline failed! Check the logs above.'
            sh 'docker compose logs || true'
        }
        always {
            echo '📊 Build finished at: ${new Date()}'
        }
    }
}
