pipeline {
    agent any

    environment {
        // Define environment variables if needed
        // Example: NODE_ENV = 'production'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend') {
            steps {
                dir('backend') {
                    script {
                        // Install dependencies
                        sh 'npm install'
                        // Optional: Run backend tests
                        // sh 'npm test'
                    }
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('frontend') {
                    script {
                        // Install dependencies
                        sh 'npm install'
                        // Build frontend
                        sh 'npm run build'
                        // Optional: Run frontend tests
                        // sh 'npm test'
                    }
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    // Build Docker images
                    sh 'docker build -t your-backend-image:latest backend/'
                    sh 'docker build -t your-frontend-image:latest frontend/'
                    // Push images to Docker registry (replace with your registry)
                    // sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                    // sh 'docker push your-backend-image:latest'
                    // sh 'docker push your-frontend-image:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Add your deployment steps here
                    // For example, use docker-compose, kubectl, or ssh to remote server
                    // sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
