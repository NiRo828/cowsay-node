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
                    parallel(
                        installCowsay: {
                            nodejs(nodeJSInstallationName: 'Node.js LTS') {
                                sh 'npm install cowsay'
                            }
                        },
                        installLolcatjs: {
                            nodejs(nodeJSInstallationName: 'Node.js LTS') {
                                sh 'npm install lolcatjs'
                            }
                        },
                        installFortune: {
                            nodejs(nodeJSInstallationName: 'Node.js LTS') {
                                sh 'npm install fortune'
                            }
                        }
                    )
                }
            }
        }
        stage('Run') {
            steps {
                dir('code') {
                    nodejs(nodeJSInstallationName: 'Node.js LTS') {
                        sh 'npm run run-nycowsay'
                    }
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




        // stage('Build') {
        //     steps {
        //         dir('code') {
        //             sh 'npm install cowsay'
        //             sh 'npm install lolcatjs'
        //             sh 'npm install fortune'
                    
        //         }
        //     }
        // }