pipeline {
    agent
        docker { 
            image 'docker:latest'
            args '-u root:root'
        }
    }

    environment {
        DOCKER_DRIVER = 'overlay2'
        NODE_IMAGE = 'node:latest'
        DOCKER_REGISTRY = 'registry.gitlab.com/pipeline2843345/pipeline .'
        IMAGE_NAME = '$DOCKER_REGISTRY/JenkinsImage'
    }

    stages {
        stage('Setup') {
            steps {
                sh '''docker login -u "vsri19" -p "glpat-pZcgBF7sx5AevPf4tamj" "$DOCKER_REGISTRY"'''
            }
        }

        stage('build') {
            steps {
                sh '''docker pull $NODE_IMAGE'''
                sh '''docker build -t $IMAGE_NAME .'''
            }
            post {
                success {
                    archiveArtifacts artifacts: 'node_modules/', allowEmptyArchive: true
                }
            }
        }
        stage('install_dependencies') {
            steps {
                sh '''docker run --rm -v $PWD:/app -w /app $NODE_IMAGE npm install'''
            }
        }
        stage('build_project') {
            steps {
                sh '''docker run --rm -v $PWD:/app -w /app $NODE_IMAGE npm run build'''
            }
        }
        stage('test') {
            steps {
                sh '''docker run --rm -v $PWD:/app -w /app $NODE_IMAGE npm test'''
            }
        }
        stage('run_project') {
            steps {
                sh '''docker run -d -p 3000:3000 --name my-node-app $IMAGE_NAME'''
                sh '''sleep 10'''
                sh '''docker ps -a'''
            }
        }
        stage('push_to_registry') {
            when {
                branch 'main'
            }
            steps {
                sh '''docker tag $IMAGE_NAME:latest $DOCKER_REGISTRY/$IMAGE_NAME:latest'''
                sh '''docker push $DOCKER_REGISTRY/$IMAGE_NAME:latest'''
            }
        }
    }
}
