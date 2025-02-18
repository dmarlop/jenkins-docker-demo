pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Clonar código') {
            steps {
                git branch: 'main', url: 'https://github.com/dmarlop/jenkins-docker-demo.git'
            }
        }
        stage('Construir imagen Docker') {
            steps {
                script {
                    dockerImage = docker.build("jenkins-docker-demo")
                }
            }
        }
        stage('Desplegar con Docker Compose') {
            steps {
                bat 'docker-compose down'
                bat 'docker-compose up -d --build'
            }
        }
    }
}

