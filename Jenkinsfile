pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('Docker-hub')
	}
        
	stages {
		
		stage('Build') {

			steps {
			  script{ 
				sh 'docker build -t 30marcel/nodeapp:0.0.1 .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push 30marcel/nodeapp:0.0.1'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
