
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Tests unitaires') {
            steps {
                dir('backend') {
                    bat 'mvn -B test'
                }
            }
        }

        stage('Build Backend') {
            steps {
                dir('backend') {
                    bat 'mvn -B package -DskipTests'
                }
            }
        }
    }

    post {
        always {
            junit 'backend/target/surefire-reports/*.xml'
        }
    }
}
