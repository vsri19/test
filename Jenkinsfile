pipeline {
  agent  {

  docker {
    image 'docker:latest'
    args '-v /c/ProgramData/Jenkins/.jenkins/workspace/test-pipeline:/workspace/test-pipeline -w /workspace/test-pipeline'
  }
}

environment {
  TEST_IMAGE = 'registry.gitlab.com/dinesh.kuswah/hello_hapi:"$CI_COMMIT_REF_NAME"'
  RELEASE_IMAGE = 'registry.gitlab.com/dinesh.kuswah/hello_hapi:latest'
}

stages {
  stage('Setup') {
    steps {
      bat 'docker login -u dinesh.kuswah@gmail.com -p 22Evz3nUHoVPSQNngqnF registry.gitlab.com/dinesh.kuswah'
    }
  }

  stage('build') {
    steps {
      bat 'docker build --pull -t $TEST_IMAGE .'
      bat 'docker push $TEST_IMAGE'
    }
  }
  stage('test') {
    steps {
      bat 'docker pull $TEST_IMAGE'
      bat 'docker run $TEST_IMAGE npm test'
    }
  }
  stage('release') {
    when {
      branch 'master'
    }
    steps {
      bat 'docker pull $TEST_IMAGE'
      bat 'docker tag $TEST_IMAGE $RELEASE_IMAGE'
      bat 'docker push $RELEASE_IMAGE'
      }
    }
  }
}
