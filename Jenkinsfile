pipeline {
    agent any

    environment {
        NODE_ENV=development
        DOCKER_USER = 'nuclearcoder26'
        DOCKER_PASS = 'dF6!aJ6@@'
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
                        // Run backend tests
                        sh 'npm test'
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
                        // Run frontend tests
                        sh 'npm test'
                    }
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    // Build Docker images
                    sh 'docker build -t nuclearcoder26/chatapp-backend:latest backend/'
                    sh 'docker build -t nuclearcoder26/chatapp-frontend:latest frontend/'
                    // Push images to Docker registry (replace with your registry)
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                    sh 'docker nuclearcoder26/chatapp-backend:latest'
                    sh 'docker nuclearcoder26/chatapp-frontend:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy using docker-compose
                    sh 'docker-compose up -d'
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