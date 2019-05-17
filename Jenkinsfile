pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                echo 'Check in' 
            }
        }
        stage('Test'){
            steps {
                echo ' Testing' 
            }
        }
        stage('Deploy') {
            steps {
                echo 'deploy'
            }
        }
    }
}
