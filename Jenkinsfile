image: node:latest

stages:
  - install
  - test

cache:
  paths:
    - node_modules/

install_dependencies:
  stage: install
  script:
    - npm install
  artifacts:
    paths:
      - node_modules/
    expire_in: 1 week

run_tests:
  stage: test
  script:
    - npm test
  dependencies:
    - install_dependencies
