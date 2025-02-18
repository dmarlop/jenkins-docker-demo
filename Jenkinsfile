pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Clonar código') {
            steps {
                // Hacemos un checkout limpio
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [[$class: 'CleanBeforeCheckout']],
                    userRemoteConfigs: [[url: 'https://github.com/dmarlop/jenkins-docker-demo.git']]
                ])
                // Imprimimos el hash del commit para confirmar la versión
                sh 'git rev-parse HEAD'
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


