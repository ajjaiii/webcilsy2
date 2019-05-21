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
<<<<<<< HEAD
                sh 'docker build -t webcilsypro .'
                sh 'docker tag webcilsypro ajjaiii/webcilsypro:$BUILD_NUMBER'
                sh 'docker push ajjaiii/webcilsypro:$BUILD_NUMBER'
               
=======
                sh 'docker build -t webcilsy .'
                sh 'docker tag webcilsy ajjaiii/webcilsy:$BUILD_NUMBER'
                sh 'docker push ajjaiii/webcilsy:$BUILD_NUMBER'
                sh 'docker image prune -fa'
>>>>>>> 20e469c70c472336af0a5edccc05a6ca3973bedd
            }
        }
        stage('Cleaning'){
            steps {
<<<<<<< HEAD
                echo 'Cleaning image'
                sh 'docker image prune -fa'
=======
                echo 'Show running pods'
                sh 'kubectl get pods'
>>>>>>> 20e469c70c472336af0a5edccc05a6ca3973bedd
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
