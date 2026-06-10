pipeline {

    agent {
        label 'linux-agent'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t fullstack-demo .'
            }
        }

        stage('Deploy') {
            steps {

                sh '''
                docker stop fullstack-demo || true

                docker rm fullstack-demo || true

                docker run -d \
                --name fullstack-demo \
                -p 3000:3000 \
                fullstack-demo
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh 'curl http://localhost:3000/health'
            }
        }
    }
}
