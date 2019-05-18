pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                echo 'Check in'
                sh 'sed -i "s/BUILD_NUMBER/$BUILD_NUMBER/g" webcilsy.yaml'
                sh 'docker build -t webcilsy .'
                sh 'docker tag webcilsy ajjjaiii/webcilsy:$BUILD_NUMBER'
                sh 'docker push ajjjaiii/webcilsy:$BUILD_NUMBER'
            }
        }
        stage('Test'){
            steps {
                echo ' Testing'
                sh 'kubectl get pods'
            }
        }
        stage('Deploy') {
            steps {
                echo 'deploy'
                sh 'kubectl apply -f webcilsy.yaml'
            }
        }
    }
}
