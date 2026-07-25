pipeline {
    agent any

    tools {
        maven 'maven_home'
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/justtbala/petclinic_war.git'
            }
        }

        stage('Build Application') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t petclinic-app .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker stop petclinic-container || true
                docker rm petclinic-container || true
                docker run -d --name petclinic-container -p 8080:8080 petclinic-app
                '''
            }
        }
    }
}
