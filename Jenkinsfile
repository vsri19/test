pipeline {
    agent any 

    stages {
        stage('install_dependencies') {
            steps {
                sh '''npm install'''
            }
        }
        stage('test') {
            steps {
                sh '''npm test'''
            }
        }
        stage('build') {
            steps {
                sh '''npm run build'''
            }
            post {
                success {
                    archiveArtifacts artifacts: 'dist/', allowEmptyArchive: true
                }
            }
        }
    }
}
