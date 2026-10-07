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

        stage('Package') {
            steps {
                bat 'powershell Compress-Archive -Path app.py,test_app.py -DestinationPath jenkins-python-demo.zip -Force'
            }
        }
    }
}