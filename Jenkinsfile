pipeline {
    agent {
        label 'linux'
    }
    options {
        skipDefaultCheckout(true)
        timestamps()
    }
    stages {
        stage('clean workspace') {
            steps {
                cleanWs()
            }
        }
        stage('checkout') {
            steps {
                checkout scm
            }
        }
        stage('terraform') {
            steps {
                sh './terraformw apply -auto-approve -no-color'
            }
        }
		stage('deterraform') {
            steps {
                sh 'terraform destroy -auto-approve'
            }
			
        }
		stage('clean workspace again') {
            steps {
                cleanWs()
            }
        }
        stage('terraform') {
            steps {
                sh './terraformw apply -auto-approve -no-color'
            }
			
        }
		stage('deterraform') {
            steps {
                sh 'terraform destroy -auto-approve'
            }
			
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
