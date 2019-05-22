pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                echo 'Building New Image'
                sh 'docker build -t ajjaiii/webcilsypro .'
                sh 'docker tag ajjaiii/webcilsypro ajjaiii/webcilsypro:$BUILD_NUMBER'
                sh 'docker push ajjaiii/webcilsypro:latest'
                sh 'docker push ajjaiii/webcilsypro:$BUILD_NUMBER'
                echo 'image has been build'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy New image to kubernetes'
                sh 'sed -i "s/BUILD_NUMBER/$BUILD_NUMBER/g" webcilsy.yaml'
                sh 'kubectl apply -f webcilsy.yaml'
                echo 'new image deployed'
            }
        }
		stage('Cleaning'){
            steps {
                echo 'Cleaning images'
                sh 'docker image prune -fa'
                echo 'images cleaned'
            }
        }
    }
}
