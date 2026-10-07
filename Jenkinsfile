// // pipeline {
// //     agent any

// //     stages {

// //         stage('Build') {
// //             steps {
// //                 bat 'python app.py'
// //             }
// //         }

// //         stage('Test') {
// //             steps {
// //                 bat 'python -m pytest'
// //             }
// //         }

// //         stage('Package') {
// //             steps {
// //                 bat 'powershell Compress-Archive -Path app.py,test_app.py -DestinationPath jenkins-python-demo.zip -Force'
// //             }
// //         }
// //     }

// //     post {
// //         success {
// //             archiveArtifacts artifacts: 'jenkins-python-demo.zip'
// //         }
// //     }
// // }


// pipeline {
//     agent any

//     stages {

//         stage('Build') {
//             steps {
//                 bat 'python app.py'
//             }
//         }

//         stage('Test') {
//             steps {
//                 bat 'python -m pytest'
//             }
//         }

//         stage('Docker Build') {
//             steps {
//                 bat 'docker build -t jenkins-python-demo .'
//             }
//         }
//     }
// }

// Jenkins+Docker



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

        stage('Docker Build') {
            steps {
                bat 'docker build -t jenkins-python-demo .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-credentials',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    bat 'docker login -u "%DOCKER_USERNAME%" -p "%DOCKER_PASSWORD%"'
                    bat 'docker tag jenkins-python-demo %DOCKER_USERNAME%/jenkins-python-demo:latest'
                    bat 'docker push %DOCKER_USERNAME%/jenkins-python-demo:latest'
                }
            }
        }
    }
}