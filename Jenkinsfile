pipeline {
    agent any

    environment {
		DOCKERHUB_CREDENTIALS=credentials('DOCKERHUB_LOGIN')
	}
    stages {
        stage('Docker Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Build & push Dockerfile') {
            steps {
                sh """
                ansible-playbook playbook.yml
                """
            }
        }
        stage('Run Dockercompose playbook') {
            steps {
                sh """
                ansible-playbook playbook-dcompose.yml 
                """
            }
        }
    }
}
