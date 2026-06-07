// pipeline {

//     agent any

//     environment {

//         FRONTEND_IMAGE = "sarvnoorkaur/frontend-app"
//         BACKEND_IMAGE  = "sarvnoorkaur/backend-app"

//     }

//     stages {

//         stage('Checkout') {

//             steps {

//                 git branch: 'main',
//                 url: 'YOUR_GITHUB_REPO_URL'

//             }
//         }

//         stage('Build Backend Image') {

//             steps {

//                 bat 'docker build -t %BACKEND_IMAGE%:latest backend'

//             }
//         }

//         stage('Build Frontend Image') {

//             steps {

//                 bat 'docker build -t %FRONTEND_IMAGE%:latest frontend'

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

//                     bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
//                 }
//             }
//         }

//         stage('Push Backend') {

//             steps {

//                 bat 'docker push %BACKEND_IMAGE%:latest'

//             }
//         }

//         stage('Push Frontend') {

//             steps {

//                 bat 'docker push %FRONTEND_IMAGE%:latest'

//             }
//         }

//     }

//     post {

//         success {

//             echo 'Images pushed to Docker Hub successfully'

//         }
//     }
// }







pipeline {

    agent any

    stages {

        stage('Checkout') {

            steps {

                git branch: 'main',
                url: 'YOUR_GITHUB_REPO_URL'

            }
        }

        stage('Compose Build & Run') {

            steps {

                bat 'docker compose up --build -d'

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

                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                }
            }
        }

        stage('Push Backend') {

            steps {

                bat 'docker push sarvnoorkaur/backend-app:latest'

            }
        }

        stage('Push Frontend') {

            steps {

                bat 'docker push sarvnoorkaur/frontend-app:latest'

            }
        }

    }

    post {

        success {

            echo 'Build, Run and Push Successful'

        }

    }

}