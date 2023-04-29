pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/NiRo828/cowsay-node.git'
            }
        }
        stage('Build') {
            steps {
                dir('code') {
                    sh 'npm install'
                }
            }
        }
        stage('Run') {
            steps {
                dir('code') {
                    sh 'npm run'
                }
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
    }
}