pipeline {
    agent any
    
    environment {
        APP_VERSION = "${env.BUILD_NUMBER}"
        DOCKER_IMAGE = "myapp:${APP_VERSION}"
        NEXUS_URL = "http://localhost:8081"
        NEXUS_USER = "admin"
        NEXUS_PASSWORD = "admin123"
    }
    
    stages {
        
        stage('Code Checkout') {
            steps {
                checkout scm
                echo "Код версии ${APP_VERSION} загружен"
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh '''
                    echo "=== Создание виртуального окружения ==="
                    python3 -m venv venv
                    . venv/bin/activate
                    
                    echo "=== Установка зависимостей ==="
                    pip install -r requirements.txt
                    pip install pytest
                    
                    echo "=== Запуск тестов ==="
                    python -m pytest test_app.py -v
                '''
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh '''
                    echo "=== Сборка Docker образа ==="
                    docker build -t ${DOCKER_IMAGE} .
                    docker tag ${DOCKER_IMAGE} myapp:latest
                    echo "Образ создан: ${DOCKER_IMAGE}"
                '''
            }
        }
        
        stage('Upload to Nexus') {
            steps {
                sh '''
                    echo "=== Упаковка приложения ==="
                    tar -czf myapp-${APP_VERSION}.tar.gz app.py requirements.txt Dockerfile
                    
                    echo "=== Загрузка в Nexus ==="
                    curl -v -u ${NEXUS_USER}:${NEXUS_PASSWORD} \
                        --upload-file myapp-${APP_VERSION}.tar.gz \
                        ${NEXUS_URL}/repository/go-binary/myapp-${APP_VERSION}.tar.gz
                '''
            }
        }
    }
    
    post {
        success {
            echo "SUCCESS: Пайплайн успешно выполнен!"
        }
        failure {
            echo "FAILURE: Проверьте логи и исправьте проблему."
        }
    }
}pipeline {pipeline {
    agent any
    
    environment {
        APP_VERSION = "${env.BUILD_NUMBER}"
        DOCKER_IMAGE = "myapp:${APP_VERSION}"
        NEXUS_URL = "http://localhost:8081"
        NEXUS_USER = "admin"
        NEXUS_PASSWORD = "admin123"
    }
    
    stages {
        
        stage('Code Checkout') {
            steps {
                checkout scm
                echo "✅ Код версии ${APP_VERSION} загружен"
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh '''
                    echo "=== Создание виртуального окружения ==="
                    python3 -m venv venv
                    . venv/bin/activate
                    
                    echo "=== Установка зависимостей ==="
                    pip install -r requirements.txt
                    pip install pytest
                    
                    echo "=== Запуск тестов ==="
                    python -m pytest test_app.py -v
                '''
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh '''
                    echo "=== Сборка Docker образа ==="
                    docker build -t ${DOCKER_IMAGE} .
                    docker tag ${DOCKER_IMAGE} myapp:latest
                    echo "Образ создан: ${DOCKER_IMAGE}"
                '''
            }
        }
        
        stage('Upload to Nexus') {
            steps {
                sh '''
                    echo "=== Упаковка приложения ==="
                    tar -czf myapp-${APP_VERSION}.tar.gz app.py requirements.txt Dockerfile
                    
                    echo "=== Загрузка в Nexus ==="
                    curl -v -u ${NEXUS_USER}:${NEXUS_PASSWORD} \
                        --upload-file myapp-${APP_VERSION}.tar.gz \
                        ${NEXUS_URL}/repository/go-binary/myapp-${APP_VERSION}.tar.gz
                '''
            }
        }
    }
    
    post {
        success {
            echo "🎉 Пайплайн успешно выполнен! Приложение готово к деплою."
        }
        failure {
            echo "❌ Ошибка! Проверьте логи и исправьте проблему."
        }
    }
}
    agent any
    
    environment {
        APP_VERSION = "${env.BUILD_NUMBER}"
        DOCKER_IMAGE = "myapp:${APP_VERSION}"
        NEXUS_URL = "http://localhost:8081"
        NEXUS_USER = "admin"
        NEXUS_PASSWORD = "admin123"
    }
    
    stages {
        
        stage('Code Checkout') {
            steps {
                checkout scm
                echo "✅ Код версии ${APP_VERSION} загружен"
            }
        }
        
        stage('Unit Tests') {
            steps {
                sh '''
                    echo "=== Установка зависимостей ==="
                    pip3 install -r requirements.txt
                    pip3 install pytest
                    
                    echo "=== Запуск тестов ==="
                    python3 -m pytest test_app.py -v
                '''
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh '''
                    echo "=== Сборка Docker образа ==="
                    docker build -t ${DOCKER_IMAGE} .
                    docker tag ${DOCKER_IMAGE} myapp:latest
                    echo "Образ создан: ${DOCKER_IMAGE}"
                '''
            }
        }
        
        stage('Upload to Nexus') {
            steps {
                sh '''
                    echo "=== Упаковка приложения ==="
                    tar -czf myapp-${APP_VERSION}.tar.gz app.py requirements.txt Dockerfile
                    
                    echo "=== Загрузка в Nexus ==="
                    curl -v -u ${NEXUS_USER}:${NEXUS_PASSWORD} \
                        --upload-file myapp-${APP_VERSION}.tar.gz \
                        ${NEXUS_URL}/repository/go-binary/myapp-${APP_VERSION}.tar.gz
                '''
            }
        }
    }
    
    post {
        success {
            echo "🎉 Пайплайн успешно выполнен! П
