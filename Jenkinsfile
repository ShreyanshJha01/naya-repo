pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', credentialsId: 'arp', url: 'https://github.com/ShreyanshJha01/naya-repo.git'
            }
        }
        stage('test') {
            steps {
                sh 'mvn test'
            }
        }
    }
    post{
        success{
            mail bcc: 'srinathpandey72@gmail.com', 
            body: """The Jenkins build has complete successfully.
            Job name: ${env.JOB_NAME}
            Build Number: ${env.BUILD_NUMBER}
            Build URL: ${env.BUILD_URL}""", cc: 'prateeksingh.ps345@gmail.com', from: '', replyTo: '', subject: 'done', to: '22051778@kiit.ac.in'
                    }
        failure{
            mail bcc: 'prateeksingh.ps345@gmail.com', body: 'this is done', cc: 'srinathpandey72@gmail.com', from: '', replyTo: '', subject: 'done', to: '22051778@kiit.ac.in'
        }
    }
}
