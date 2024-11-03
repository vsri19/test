pipeline {
    agent {
        docker { image 'docker:latest' }
    }

    environment {
        TEST_IMAGE = "registry.gitlab.com/dinesh.kuswah/hello_hapi:${env.BRANCH_NAME}"
        RELEASE_IMAGE = 'registry.gitlab.com/dinesh.kuswah/hello_hapi:latest'
    }

    stages {
        stage('Setup') {
            steps {
                sh 'docker login -u dinesh.kuswah@gmail.com -p 22Evz3nUHoVPSQNngqnF registry.gitlab.com/dinesh.kuswah'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build --pull -t $TEST_IMAGE .'
                sh 'docker push $TEST_IMAGE'
            }
        }

        stage('Test') {
            steps {
                sh 'docker pull $TEST_IMAGE'
                sh 'docker run $TEST_IMAGE npm test'
            }
        }

        stage('Release') {
            when {
                branch 'master'
            }
            steps {
                sh 'docker pull $TEST_IMAGE'
                sh 'docker tag $TEST_IMAGE $RELEASE_IMAGE'
                sh 'docker push $RELEASE_IMAGE'
            }
        }
    }
}
