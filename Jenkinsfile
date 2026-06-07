pipeline {

    agent any

    environment {

        FRONTEND_IMAGE = "sarvnoorkaur/frontend-app"
        BACKEND_IMAGE  = "sarvnoorkaur/backend-app"

    }

    stages {

        stage('Checkout') {

            steps {

                git branch: 'main',
                url: 'https://github.com/Sarvnoor-kaur/dockercompose-jenkins.git'

            }
        }

        stage('Build Backend Image') {

            steps {

                sh 'docker build -t %BACKEND_IMAGE%:latest backend'

            }
        }

        stage('Build Frontend Image') {

            steps {

                sh 'docker build -t %FRONTEND_IMAGE%:latest frontend'

            }
        }

        stage('Docker Login') {

            steps {

                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {

                    sh 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                }
            }
        }

        stage('Push Backend') {

            steps {

                sh 'docker push %BACKEND_IMAGE%:latest'

            }
        }

        stage('Push Frontend') {

            steps {

                sh 'docker push %FRONTEND_IMAGE%:latest'

            }
        }

    }

    post {

        success {

            echo 'Images pushed to Docker Hub successfully'

        }
    }
}







// pipeline {

//     agent any

//     stages {

//         stage('Checkout') {

//             steps {

//                 git branch: 'main',
//                 url: 'https://github.com/Sarvnoor-kaur/dockercompose-jenkins.git'

//             }
//         }

//         stage('Compose Build & Run') {

//             steps {

//                 sh 'docker compose up --build -d'

//             }
//         }

//         stage('Docker Login') {

//             steps {

//                 withCredentials([
//                     usernamePassword(
//                         credentialsId: 'dockerhub',
//                         usernameVariable: 'DOCKER_USER',
//                         passwordVariable: 'DOCKER_PASS'
//                     )
//                 ]) {

//                     sh 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
//                 }
//             }
//         }

//         stage('Push Backend') {

//             steps {

//                 sh 'docker push sarvnoorkaur/backend-app:latest'

//             }
//         }

//         stage('Push Frontend') {

//             steps {

//                 sh 'docker push sarvnoorkaur/frontend-app:latest'

//             }
//         }

//     }

//     post {

//         success {

//             echo 'Build, Run and Push Successful'

//         }

//     }

// }