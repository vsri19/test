pipeline {
    agent {
        docker { image 'node:22.11.0-alpine3.20' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
            }
        }
    }
}
