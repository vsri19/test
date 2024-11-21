pipeline {
    agent {
        docker {
            image 'node:16'
            args '-u root:root'
        }
    }

    stages {
        stage('install_dependencies') {
            when {
                expression { env.CI_COMMIT_BRANCH == env.CI_DEFAULT_BRANCH }
            }
            steps {
                sh 'npm install'
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
