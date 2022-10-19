pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-hub')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t 30marcel/nodeapp:1.0.0 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push 30marcel/nodeapp:1.0.0'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
