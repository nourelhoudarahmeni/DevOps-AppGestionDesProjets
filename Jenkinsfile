
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
                withEnv([
                    'JAVA_HOME=C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.16.8-hotspot',
                    'PATH+JDK=C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.16.8-hotspot\\bin',
                    'PATH+MAVEN=C:\\Users\\nawres\\apache-maven-3.9.14\\bin'
                ]) {
                    dir('backend') {
                        bat 'java -version'
                        bat 'mvn -version'
                        bat 'mvn -B test'
                    }
                }
            }
        }

        stage('Build Backend') {
            steps {
                withEnv([
                    'JAVA_HOME=C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.16.8-hotspot',
                    'PATH+JDK=C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.16.8-hotspot\\bin',
                    'PATH+MAVEN=C:\\Users\\nawres\\apache-maven-3.9.14\\bin'
                ]) {
                    dir('backend') {
                        bat 'mvn -B package -DskipTests'
                    }
                }
            }
        }
    }

    post {
        always {
            junit allowEmptyResults: true,
                  testResults: 'backend/target/surefire-reports/*.xml'
        }
    }
}
