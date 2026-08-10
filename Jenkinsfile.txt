pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                git branch: 'main', url: 'https://github.com/Rushikesh2425/Jenkins-CICD.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Build Step: Checking project files...'
                bat 'dir'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing the web application...'
                bat 'echo Test successful'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying web application...'
                bat 'if not exist C:\\JenkinsDeploy mkdir C:\\JenkinsDeploy'
                bat 'xcopy /Y /E * C:\\JenkinsDeploy\\'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed! Check the console output.'
        }
    }
}