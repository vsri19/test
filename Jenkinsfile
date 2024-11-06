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

        stage('Run Tests') {
            steps {
                // Run npm tests
                script {
                    echo 'Running npm test...'
                    sh 'npm test'
                }
            }
        }
    }

    post {
        always {
            // Archive test results if available
            junit '**/test-results.xml' // Modify this pattern based on where your tests output XML results
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
