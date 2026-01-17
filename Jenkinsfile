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
                    sh 'mvn clean compile'
                }
            }
        }

        stage('SonarQube Scan') {
            steps {
                dir('pipeline') {
                    withSonarQubeEnv('sonar_banaye_chinar') {
                        sh '''
                        mvn clean verify \
                        org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
                        -Dsonar.projectKey=pipeline-project \
                        -Dsonar.projectName=pipeline-project
                        '''
                    }
                }
            }
        }
    }
}
