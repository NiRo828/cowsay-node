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
                    sh 'npm build'
                }
            }
        }
        stage('Run') {
            steps {
                dir('code') {
                    sh 'npm start'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
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
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}

