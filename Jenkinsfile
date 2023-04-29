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
                    sh 'npm install cowsay'
                    sh 'npm install lolcatjs'
                    sh 'npm install fortune'
                    
                }
            }
        }
        stage('Run') {
            steps {
                dir('code') {
                    sh 'npm run fortune | cowsay | lolcatjs '
                }
            }
        }
        stage('SonarQube Analysis') {
            steps {
                def scannerHome = tool 'SonarScanner';
                withSonarQubeEnv(credentialsId: 'CowSaySQToken') {
                    sh "${scannerHome}/bin/sonar-scanner"
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



