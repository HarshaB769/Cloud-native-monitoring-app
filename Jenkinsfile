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
                sh 'cloud-native-monitoring-app:v1 .'
            }
        }

        stage('Deploy App') {
            steps {
                sh '''
                docker stop cloud-native-monitoring-app:v1 || true
                docker rm cloud-native-monitoring-app:v1 || true

                docker run -d \
                  --name cloud-native-monitoring-app \
                  -p 5000:5000 \
                  -e PORT=${PORT} \
                  cloud-native-monitoring-app
                '''
            }
        }
    }
}
