pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/HarshaB769/Cloud-native-monitoring-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cloud-native-monitoring-app  .'
            }
        }

        stage('Deploy App') {
            steps {
                sh '''
                docker stop cloud-native-monitoring-app || true
                docker rm cloud-native-monitoring-app || true

                docker run -d \
                  --name cloud-native-monitoring-app \
                  -p 9000:9000 \
                  -e PORT=${PORT} \
                  cloud-native-monitoring-app
                '''
            }
        }
    }
}
