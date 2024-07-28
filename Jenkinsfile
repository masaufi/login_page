pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/masaufi/login_page.git', branch: 'master'
            }
        }
        
        stage('Build and Deploy with Docker Compose') {
            steps {
                script {
                    dockerCompose.up '--build -d'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    docker.image('masaufi/login_page:latest').inside {
                        sh 'npm install'
                        sh 'npm test'
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deployment steps would go here.'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
