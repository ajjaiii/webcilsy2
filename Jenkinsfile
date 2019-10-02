pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                echo 'Building New Image'
                sh 'ls -al'
                sh 'sed -i "s/BUILD_NUMBER/$BUILD_NUMBER/g" webcilsy.yaml'
                sh 'docker build -t webcilsy .'
                sh 'docker tag webcilsy ajjaiii/webcilsy:$BUILD_NUMBER'
                sh 'docker push ajjaiii/webcilsy:$BUILD_NUMBER'
               
            }
        }
        stage('Cleaning'){
            steps {
                echo 'Cleaning image'
                sh 'docker image prune -fa'
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
