pipeline {
    agent any
    environment {
		DOCKERHUB_CREDENTIALS=credentials('d0735951-89cf-476e-a48d-7a011873183b')
	}
    stages {
        stage('Cloning Git') {
          steps {
              git([url: 'https://github.com/timohito/SSPR-dotnet.git', branch: 'main'])
          }
        }
        stage('Build') {

			steps {
				sh 'docker build -t timurok73/sspr:latest .'
			}
		}

        stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push timurok73/sspr:latest'
			}
		}
    }
    post {
		always {
			sh 'docker logout'
		}
	}
}
