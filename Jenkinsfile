pipeline {
    agent {
        docker {
            image 'node:16'
            args '-u root:root'
        }
    }

    stages {
        stage('install_dependencies') {
            steps {
                sh 'cd $WORKSPACE npm install'
                sh 'npm --version'
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
