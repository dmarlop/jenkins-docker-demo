pipeline {
    agent any

    stages {
        stage('Clonar código') {
            steps {
                git branch: 'main', url: 'https://github.com/tu-usuario/jenkins-docker-demo.git'
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
                sh 'docker-compose down'
                sh 'docker-compose up -d --build'
            }
        }
    }
}
