pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Madhuri-Chavan-12/CI-CD.git'
            }
        }

        stage('Run Application') {
            steps {
                sh 'python3 Calculator.py'
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
