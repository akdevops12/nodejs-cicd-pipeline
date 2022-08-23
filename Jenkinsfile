pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('Docker-hub')
	}
        
	stages {
		
		stage('Build') {

			steps {
				sh 'docker build -t 30marcel/nodeapp:v2 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push 30marcel/nodeapp:v2'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
