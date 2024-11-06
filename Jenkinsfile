pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/yourusername/hello-world-app.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Build') {
            steps {
                sh 'npm start &'
            }
        }
    }
    post {
        success {
            emailext(
                subject: "Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                Build #${env.BUILD_NUMBER} of ${env.JOB_NAME} was successful!

                Check the details at ${env.BUILD_URL}
                """,
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            )
            echo 'Application deployed successfully!'
        }
        failure {
            emailext(
                subject: "Build Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                Build #${env.BUILD_NUMBER} of ${env.JOB_NAME} failed.

                Check the console output for details: ${env.BUILD_URL}
                """,
                recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            )
            echo 'Build failed!'
        }
    }
}

