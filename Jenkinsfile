pipeline {
    agent any

    environment {
        IMAGE_NAME = 'k4k010/cloud-flask-app'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/kaustubh0010/cloud-flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push $IMAGE_NAME'
                    sh 'docker logout'
                }
            }
        }

        stage('Deploy to Server') {
            steps {
                sshagent(['server-ssh']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no user@your-server-ip << EOF
                        docker pull $IMAGE_NAME
                        docker stop flask-app || true
                        docker rm flask-app || true
                        docker run -d --name flask-app -p 5000:5000 $IMAGE_NAME
                        EOF
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace....'
            cleanWs()
        }
    }
}
