pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '"C:\\Users\\Aryan Atharv\\AppData\\Local\\Programs\\Python\\Python314\\python.exe" -m pip install pytest --quiet'
            }
        }

        stage('Run Tests') {
            steps {
                bat '"C:\\Users\\Aryan Atharv\\AppData\\Local\\Programs\\Python\\Python314\\python.exe" -m pytest test_calculator.py -v --junitxml=results.xml'
            }
        }

        stage('Build Complete') {
            steps {
                echo 'Build finished successfully!'
            }
        }
    }

    post {
        always {
            junit 'results.xml'
        }

        success {
            emailext(
                to: 'iheckinlovetenzkekw@gmail.com',
                subject: "BUILD PASSED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "<h2>Build Successful!</h2>",
                mimeType: 'text/html'
            )
        }

        failure {
            emailext(
                to: 'iheckinlovetenzkekw@gmail.com',
                subject: "BUILD FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "<h2>Build Failed!</h2>",
                mimeType: 'text/html'
            )
        }
    }
}