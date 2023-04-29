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
        // stage('Test') {
        //     steps {
        //         dir('code') {
        //             sh 'npm test'
        //         }
        //     }
        // }
        // stage('Build Docker Image') {
        //     steps {                
        //         dir('code') {
        //             sh 'docker build -t cowsay-node .'
        //         }                
        //     }
        // }
        stage('Run') {
            steps {
                dir('code') {
                    sh 'npm run'
                }
            }
        }
        stage('Test') {
            steps {
                dir('code') {
                    sh 'curl -s http://localhost:8080 | grep "Welcome to Node.js v"'
                }
            }
        }
        stage('Deploy') {
            steps {
                dir('code') {
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                    sh 'docker tag cowsay-node $DOCKER_USER/cowsay-node:$BUILD_NUMBER'
                    sh 'docker push $DOCKER_USER/cowsay-node:$BUILD_NUMBER'
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

