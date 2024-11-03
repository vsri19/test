pipeline {
  agent  {

  docker {
    image 'docker:latest'
  }
}

environment {
  TEST_IMAGE = 'registry.gitlab.com/dinesh.kuswah/hello_hapi:"$CI_COMMIT_REF_NAME"'
  RELEASE_IMAGE = 'registry.gitlab.com/dinesh.kuswah/hello_hapi:latest'
}

stages {
  stage('Setup') {
    steps {
      sh ''
      'docker login -u dinesh.kuswah@gmail.com -p 22Evz3nUHoVPSQNngqnF registry.gitlab.com/dinesh.kuswah'
      ''
    }
  }

  stage('build') {
    steps {
      sh ''
      'docker build --pull -t $TEST_IMAGE .'
      ''
      sh ''
      'docker push $TEST_IMAGE'
      ''
    }
  }
  stage('test') {
    steps {
      sh ''
      'docker pull $TEST_IMAGE'
      ''
      sh ''
      'docker run $TEST_IMAGE npm test'
      ''
    }
  }
  stage('release') {
    when {
      branch 'master'
    }
    steps {
      sh ''
      'docker pull $TEST_IMAGE'
      ''
      sh ''
      'docker tag $TEST_IMAGE $RELEASE_IMAGE'
      ''
      sh ''
      'docker push $RELEASE_IMAGE'
      ''
      }
    }
  }
}
