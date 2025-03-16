pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "jenkinspipeline:latest"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/jacktherizzler/JenkinsPipeline.git'
            }
        }

        stage('Build Backend') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE ./backend'
            }
        }

        stage('Run SonarQube Analysis') {
            steps {
                sh 'sonar-scanner'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'docker run --rm $DOCKER_IMAGE pytest'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
