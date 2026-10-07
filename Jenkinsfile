pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                bat 'python app.py'
            }
        }

        stage('Test') {
            steps {
                bat 'python -m pytest'
            }
        }
    }
}