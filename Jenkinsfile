pipeline {
    agent {
        label 'linux'
    }
    options {
        skipDefaultCheckout(true)
        timestamps()
    }
    stages {
        stage('clean workspace 01') {
            steps {
                cleanWs()
            }
        }
        stage('checkout') {
            steps {
                checkout scm
            }
        }
        stage('terraform 01') {
            steps {
                sh './terraformw apply -auto-approve -no-color'
            }
        }
		stage('deterraform 01') {
            steps {
                sh './terraform destroy -auto-approve'
            }
			
        }
		stage('clean workspace again') {
            steps {
                cleanWs()
            }
        }
        stage('terraform 02') {
            steps {
                sh './terraformw apply -auto-approve -no-color'
            }
			
        }
		stage('deterraform 02') {
            steps {
                sh './terraform destroy -auto-approve'
            }
			
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
