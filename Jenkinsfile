pipeline {
    agent { label 'dev' }

    stages {

        stage('Checkout Jenkinsfile Repo') {
            steps {
                checkout scm
            }
        }

        stage('Checkout Project Repo') {
            steps {
                dir('project') {
                    git branch: 'main',
                        credentialsId: 'github-creds',
                        url: 'https://github.com/ShreyanshJha01/pipeline.git'
                }
            }
        }

        stage('Build Project') {
            steps {
                dir('project') {
                    sh 'ls -la'
                    sh 'chmod +x mvnw'
                    sh './mvnw clean compile'
                }
            }
        }

        stage('SonarQube Scan') {
            steps {
                dir('project') {
                    withSonarQubeEnv('sonar-cred-s') {
                        sh './mvnw sonar:sonar'
                    }
                }
            }
        }
    }
}
