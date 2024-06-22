pipeline {
    agent any
    environment {
        DJANGO_SETTINGS_MODULE = 'todo.settings'
        DOCKER_IMAGE = 'todo'
        REGISTRY_CREDENTIALS = credentials('manishpawar')
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("$DOCKER_IMAGE:${env.BUILD_ID}")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'manishpawar') {
                        docker.image("$DOCKER_IMAGE:${env.BUILD_ID}").push('latest')
                    }
                }
            }
        }
    }
}
