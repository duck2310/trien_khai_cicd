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
                dir('paintshop/paintshop') {
                    bat 'mvn clean install'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('paintshop/paintshop') {
                    withSonarQubeEnv('SonarLocal') {
                        bat "${env.SONARQUBE_SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=paintshop -Dsonar.sources=src -Dsonar.java.binaries=target"
                    }
                }
            }
        }

        stage('Test') {
            steps {
                dir('paintshop/paintshop') {
                    bat 'mvn test'
                }
            }
        }
    }
}
