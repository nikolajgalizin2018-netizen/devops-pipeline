pipeline {
    agent any
    
    environment {
        APP_VERSION = "${env.BUILD_NUMBER}"
        DOCKER_IMAGE = "myapp:${APP_VERSION}"
        NEXUS_URL = "http://192.168.1.100:8081"
        NEXUS_USER = "admin"
        NEXUS_PASSWORD = "admin123"
    }
    
    stages {
        
        stage('Code Checkout') {
            steps {
                checkout scm
                echo "Code version ${APP_VERSION} loaded"
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh '''
                    echo "Create virtual environment"
                    python3 -m venv venv
                    . venv/bin/activate
                    
                    echo "Install dependencies"
                    pip install -r requirements.txt
                    pip install pytest
                    
                    echo "Run tests"
                    python -m pytest test_app.py -v
                '''
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh '''
                    echo "Building Docker image"
                    docker build -t ${DOCKER_IMAGE} .
                    docker tag ${DOCKER_IMAGE} myapp:latest
                    echo "Image created: ${DOCKER_IMAGE}"
                '''
            }
        }
        
        stage('Upload to Nexus') {
            steps {
                sh '''
                    echo "Package application"
                    tar -czf myapp-${APP_VERSION}.tar.gz app.py requirements.txt Dockerfile
                    
                    echo "Upload to Nexus"
                    curl -v -u ${NEXUS_USER}:${NEXUS_PASSWORD} \
                        --upload-file myapp-${APP_VERSION}.tar.gz \
                        ${NEXUS_URL}/repository/go-binary/myapp-${APP_VERSION}.tar.gz
                '''
            }
        }
    }
    
    post {
        success {
            echo "SUCCESS: Pipeline completed!"
        }
        failure {
            echo "FAILURE: Check logs!"
        }
    }
}
