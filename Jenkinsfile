pipeline {
    agent any

    environment {
        FRONTEND_DIR = 'travelbuddy'
        BACKEND_DIR = 'spring'
    }

    stages {
        stage('Checkout') {
            steps {
                
                checkout scm
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir(FRONTEND_DIR) {
                    script {
                        echo 'Installing frontend dependencies...'
                        sh 'npm install' 
                    }
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir(FRONTEND_DIR) {
                    script {
                        echo 'Building frontend application...'
                        sh 'npm run build --prod' 
                    }
                }
            }
        }

        stage('Build Backend') {
            steps {
                dir(BACKEND_DIR) {
                    script {
                        echo 'Building backend application using Maven...'
                        sh 'mvn clean install -DskipTests'
                    }
                }
            }
        }

        
        stage('Dockerize Frontend') {
            steps {
                dir(FRONTEND_DIR) {
                    script {
                        echo 'Building Docker image for frontend...'
                        sh 'docker build -t my-angular-app .' // Dockerize Angular app
                    }
                }
            }
        }

        stage('Dockerize Backend') {
            steps {
                dir(BACKEND_DIR) {
                    script {
                        echo 'Building Docker image for backend...'
                        sh 'docker build -t my-spring-boot-app .' // Dockerize Spring Boot app
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging environment...'
                    // Add deployment logic for staging environment
                    // Example: sh './deploy_staging.sh'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production environment...'
                    // Add deployment logic for production environment
                    // Example: sh './deploy_production.sh'
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up resources...'
            // Any post-build cleanup actions (e.g., remove temporary files)
        }
        success {
            echo 'Build and deployment were successful!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
