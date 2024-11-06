pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                script {
                    echo 'Running npm install...'
                    sh 'npm install'
                }
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
