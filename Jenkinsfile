#!groovy
node ('master'){
	currentBuild.result = "SUCCESS"
		stage 'Github checking'
			git branch: 'production',
            credentialsId: 'github',
            url: 'https://github.com/ajjaiii/webcilsy2.git'
			echo 'file checked out'
		stage 'Build'
			node ('master'){
				git branch: 'production',
                credentialsId: 'github',
                url: 'https://github.com/ajjaiii/webcilsy2.git'
				print "Running on : ${env.NODE_NAME}"

				echo 'Building Image'
				sh 'sed -i "s/BUILD_NUMBER/$BUILD_NUMBER/g" webcilsy.yaml'
				sh 'docker build . -t ajjaiii/webcilsypro'
				sh 'docker tag ajjaiii/webcilsypro ajjaiii/webcilsypro:$BUILD_NUMBER'
                                sh 'docker login'
                                sh 'docker push ajjaiii/webcilsypro:latest'
				sh 'docker push ajjaiii/webcilsypro:$BUILD_NUMBER'
                                echo 'image has been build'
				
			}
		stage 'Cleaning'
			echo 'Cleaning image'
			print "branch : ${env.BRANCH_NAME}"
			sh 'docker image prune -fa'
			echo 'image cleaned'
			
		stage 'Deploy'
			echo 'Deploying Aplication'
			print "branch : ${env.BRANCH_NAME}"
			sh 'kubectl apply -f webcilsy.yaml'
			echo 'website deployed'
}
