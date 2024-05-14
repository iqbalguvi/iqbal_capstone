pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t my-react-app .'
            }
        }
        stage('Push to Docker Hub (Dev)') {
            when {
                branch 'dev'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'Docker-hub', usernameVariable: 'iqbalguvi', passwordVariable: 'Hena@7152')]) {
                    sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                    sh "docker tag my-react-app $DOCKER_USERNAME/dev:latest"
                    sh "docker push $DOCKER_USERNAME/dev:latest"
                }
            }
        }
        stage('Push to Docker Hub (Prod)') {
            when {
                branch 'master'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'Docker-hub', usernameVariable: 'iqbalguvi', passwordVariable: 'Hena@7152')]) {
                    sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                    sh "docker tag my-react-app $DOCKER_USERNAME/prod:latest"
                    sh "docker push $DOCKER_USERNAME/prod:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
