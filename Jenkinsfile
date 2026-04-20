pipeline {
    agent any

    environment {
        IMAGE_NAME = "nginx-devops-app"
        TARGET_SERVER = "sysadmin@10.20.151.69"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rohits-bw/sample-nginx-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Save Image') {
            steps {
                sh 'docker save $IMAGE_NAME > app.tar'
            }
        }

        stage('Deploy to Server') {
            steps {
                sh '''
                scp -o StrictHostKeyChecking=no app.tar $TARGET_SERVER:/tmp/
                ssh -o StrictHostKeyChecking=no $TARGET_SERVER "
                    docker load < /tmp/app.tar &&
                    docker stop nginx-app || true &&
                    docker rm nginx-app || true &&
                    docker run -d -p 80:80 --name nginx-app $IMAGE_NAME
                "
                '''
            }
        }
    }
}
