pipeline {
    agent any

    environment {
        PATH = "/opt/homebrew/bin:/usr/local/bin:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'python3 -m pip install -r requirements.txt --break-system-packages'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'python3 -m test_calculator.py -v'
            }
        }
    }

    post {
        success {
            echo 'All tests passed!'
        }
        failure {
            echo 'Tests failed — check console output above for details.'
        }
    }
}
