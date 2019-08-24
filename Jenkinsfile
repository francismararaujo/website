pipeline {
  agent {
    docker {
      image 'nexaoo/jekyll'
    }

  }
  stages {
    stage('Tests') {
      steps {
        sh 'rake test:website'
      }
    }
    stage('Publish') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_nexaoo') {
            def websiteImage = docker.build("nexaoo/cyriltavian:${env.BUILD_ID}", "-f ./docker/dockerfile .")
            websiteImage.push()
          }
        }

      }
    }
  }
  environment {
    LC_ALL = 'C.UTF-8'
  }
}