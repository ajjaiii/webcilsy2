pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                echo 'Building New Image'
                sh 'sed -i "s/BUILD_NUMBER/$BUILD_NUMBER/g" webcilsy.yaml'
                sh 'docker build -t webcilsy .'
                sh 'docker tag webcilsy ajjaiii/webcilsy:$BUILD_NUMBER'
                sh 'docker push ajjaiii/webcilsy:$BUILD_NUMBER'
            }
        }
        stage('Test'){
            steps {
                echo 'Show running pods'
                sh 'kubectl get pods'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy New image to kubernetes'
                sh 'kubectl apply -f webcilsy.yaml'
            }
        }
    }
}
