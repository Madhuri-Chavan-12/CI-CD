pipeline {
    agent any
    stages {

        stage('Checkout code'){
            steps {
                git branch: 'main',
                url: 'https://github.com/Madhuri-Chavan-12/CI-Cd.git'
            }
        }

        stage('Run Application'){
            steps {
                sh 'python3 app.py'
            }
        }
    }

    post {
        success{
            echo 'Pipeline Success'
        }

        failure {
            echo 'Pipeline Failed'
        }
    }
}