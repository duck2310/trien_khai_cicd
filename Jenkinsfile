pipeline {
    agent any

    tools {
        maven 'Maven 3.9.11'
    }

    environment {
        SONARQUBE_SCANNER_HOME = tool 'SonarScanner'
    }

    stages {
        stage('Build') {
            steps {
                dir('paintshop') {
                    bat 'mvn clean install'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('paintshop') {
                    withSonarQubeEnv('mysonar') {
                        bat "${env.SONARQUBE_SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=paintshop -Dsonar.sources=src -Dsonar.java.binaries=target"
                    }
                }
            }
        }

        stage('Test') {
            steps {
                dir('paintshop') {
                    bat 'mvn test'
                }
            }
        }
    }
}
