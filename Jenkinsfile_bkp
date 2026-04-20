pipeline {
    agent any

    environment {
        WEB_SERVER = "sysadmin@10.20.151.69"
    }

    stages {

        stage('Clone Code') {
            steps {
                echo "Code already checked out by Jenkins"
            }
        }

        stage('Build') {
            steps {
                echo "No build required for static HTML"
            }
        }

        stage('Test') {
            steps {
                echo "Running basic test"
                sh 'cat index.html'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                scp -o StrictHostKeyChecking=no index.html $WEB_SERVER:/tmp/
                ssh -o StrictHostKeyChecking=no $WEB_SERVER "sudo mv /tmp/index.html /var/www/html/index.html"
                '''
            }
        }
    }
}
