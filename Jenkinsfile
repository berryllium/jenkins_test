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
        stage('Clean Up') {
            steps {
                script {
                    // Удаление старого контейнера, если он существует
                    sh '''
                    if [ "$(docker ps -q -f name=my-php-app)" ]; then
                        echo "Removing existing container..."
                        docker rm -f my-php-app
                    else
                        echo "No existing container to remove."
                    fi
                    '''

                    // Удаление старого образа, если он существует
                    sh '''
                    if [ "$(docker images -q my-php-app)" ]; then
                        echo "Removing existing image..."
                        docker rmi -f my-php-app
                    else
                        echo "No existing image to remove."
                    fi
                    '''
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
