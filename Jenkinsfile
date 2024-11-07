pipeline {
    agent any

        any
    }

    stages {
        stage('test') {
        docker { image 'postgres:alpine' }
                }
            steps {
                environment {
                    POSTGRES_DB = 'custom_db'
                    POSTGRES_USER = 'custom_user'
                    POSTGRES_PASSWORD = 'custom_pass'
                }
                sh '''export DATABASE_URL=postgres://$POSTGRES_USER:$POSTGRES_PASSWORD@postgres:5432/$POSTGRES_DB'''
                sh '''apt-get update -qy'''
                sh '''apt-get install -y python-dev python-pip'''
                sh '''pip install -r requirements.txt'''
                sh '''python manage.py test'''
            }
        }
        stage('staging') {
            when {
                branch 'master'
            }
            steps {
                sh '''apt-get update -qy'''
                sh '''apt-get install -y ruby-dev'''
                sh '''gem install dpl'''
                sh '''dpl --provider=heroku --app=$HEROKU_STAGING_APP --api-key=$HEROKU_STAGING_API_KEY --skip-cleanup'''
            }
        }
        stage('production') {
            when {
                tag pattern '.*', comparator 'REGEXP'
            }
            steps {
                sh '''apt-get update -qy'''
                sh '''apt-get install -y ruby-dev'''
                sh '''gem install dpl'''
                sh '''dpl --provider=heroku --app=$HEROKU_PRODUCTION_APP --api-key=$HEROKU_PRODUCTION_API_KEY --skip-cleanup'''
            }
        }
    }
}
