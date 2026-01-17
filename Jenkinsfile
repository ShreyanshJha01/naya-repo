pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('scanning') {
            steps {
                withSonarQubeEnv(
                    installationName: 'sonar_banaye_chinar',
                    credentialsId: 'sonar_banaega_chinar'
                ) {
                    sh 'mvn clean verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar'
                }
            }
        }
    }
}
