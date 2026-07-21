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
        sh 'python3 -m pytest test_calculator.py -v'
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
    post {
    success {
        mail to: 'ydivyansh68@gmail.com',
             subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
             body: "Good news — the build ${env.BUILD_NUMBER} for ${env.JOB_NAME} completed successfully.\n\nCheck it out: ${env.BUILD_URL}"
    }
    failure {
        mail to: 'ydivyansh68@gmail.com',
             subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
             body: "The build ${env.BUILD_NUMBER} for ${env.JOB_NAME} failed.\n\nCheck the console output: ${env.BUILD_URL}console"
    }
}
}
