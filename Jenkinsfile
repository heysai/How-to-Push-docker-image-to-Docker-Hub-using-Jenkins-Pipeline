pipeline{

	agent {label 'linux'}

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerpipeline')
	}

	stages {
	    
	    stage('gitclone') {

			steps {
				git 'https://github.com/heysai/nodeapp_test.git'
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t whatsup108/nodeapp_test:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push whatsup108/nodeapp_test:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}
