pipeline {
    agent {
        docker {
            image 'node:16'
        }
    }

    stages {
        stage('install_dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('build') {
            steps {
                sh 'npm run build'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'dist/', allowEmptyArchive: true
                }
            }
        }
    }
}
