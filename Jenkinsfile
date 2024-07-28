pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'masaufi/login_page:latest'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/masaufi/login_page.git', branch: 'main'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        
        stage('Run Tests') {
            steps {
                script {
                    docker.image(DOCKER_IMAGE).inside {
                        sh 'npm install'
                        sh 'npm test'
                    }
                }
            }
        }
        
        stage('Deploy with Docker Compose') {
            steps {
                script {
                    sh 'docker-compose up --build -d'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
