pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                sh 'exit 1'
            }
        }
    }

    post {
        failure {
            emailext(
                subject: "Build Failed: ${env.JOB_NAME}",
                body: """
                Build Failed

                Job: ${env.JOB_NAME}
                Build Number: ${env.BUILD_NUMBER}

                URL:
                ${env.BUILD_URL}
                """,
                to: 'madhurichavan612@gmail.com'
            )
        }
    }
}
