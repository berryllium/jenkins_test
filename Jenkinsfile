pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Собираем Docker-образ с тегом my-php-app
                    sh 'docker build -t my-php-app .'
                }
            }
        }
        stage('Run') {
            steps {
                script {
                    // Проверяем, запущен ли контейнер, если да, останавливаем его
                    sh '''
                    if [ $(docker ps -q -f name=my-php-app) ]; then
                        docker stop my-php-app && docker rm my-php-app
                    fi
                    '''
                    // Запускаем контейнер на порту 8080
                    sh 'docker run -d -p 8080:80 --name my-php-app my-php-app'
                }
            }
        }
    }
}
