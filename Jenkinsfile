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
        success {
            echo 'Pipeline Success'
        }

        failure {
            echo 'Pipeline Failed'
        }
    }
}