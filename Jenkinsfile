pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Greet User') {
            steps {
                sh 'echo "Hello, User!"'
            }
        }

        stage('Build') {
            steps {
                sh 'ls -la'
            }
        }
    }
    
}