pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build -t akloud12/nodeapp:1.0.0 .'
			}
		}


		stage('Sonarqube Analysis') {
			environment {
				SCANNER_HOME= tool 'Sonar-scanner'
			}

			steps {
			withSonarQubeEnv(credentialsId: 'sonar-credentialsId', installationName: 'Sonar') {
         sh '''$SCANNER_HOME/bin/sonar-scanner \
         -Dsonar.projectKey=projectKey \
         -Dsonar.projectName=projectName \
         -Dsonar.sources=src/ \
         -Dsonar.java.binaries=target/classes/ \
         -Dsonar.exclusions=src/test/java/****/*.java \
         -Dsonar.java.libraries=/var/lib/jenkins/.m2/**/*.jar \
         -Dsonar.projectVersion=${BUILD_NUMBER}-${GIT_COMMIT_SHORT}'''
			}
		}
        stage('SQuality Gate') {
          steps {
            timeout(time: 1, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
            }
  }
}




		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push akloud12/nodeapp:1.0.0'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
