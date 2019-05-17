pipeline {
  agent {
    docker {
      image 'ajjaiii/webcilsy'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh '''docker build . -t webcilsy
docker tag webcilsy ajjaiii/webcilsy:$BUILD_NUMBER
docker push ajjaiii/webcilsy:$BUILD_NUMBER

docker run -d -p 80:80 --name webcilsy ajjaiii/webcilsy:$BUILD_NUMBER'''
      }
    }
  }
}