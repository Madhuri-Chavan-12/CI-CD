pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                sh 'exit 1'
            }
        }
    }

    post {
        failure {
            emailext(
                to: 'madhurichavan612@gmail.com',
                subject: 'Build Failed',
                body: 'Build Failed'
            )
        }
    }
}
