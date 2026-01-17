pipeline {
    agent {
        label 'dev'
    }

    stages {

        stage('Checkout Pipeline Repo') {
            steps {
                checkout scm
            }
        }

        stage('Clone Project Repo') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-creds',
                    url: 'https://github.com/ShreyanshJha01/pipeline.git'
            }
        }

        stage('Build Project') {
            steps {
                dir('pipeline') {
                    sh 'chmod +x mvnw'
                    sh './mvnw clean compile'
                }
            }
        }


        stage('SonarQube Scan') {
            steps {
                dir('pipeline') {
                    withSonarQubeEnv('sonar-cred-s') {
                        sh './mvnw sonar:sonar'
                    }
                }
            }
        }
    }
}
