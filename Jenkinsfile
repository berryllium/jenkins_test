pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Сборка нового Docker образа
                    docker.build('my-php-app')
                }
            }
        }
        stage('Run New Container') {
            steps {
                script {
                    // Запуск нового контейнера
                    docker.image('my-php-app').run('-d -p 8888:80 --name my-php-app')
                }
            }
        }
    }
}
