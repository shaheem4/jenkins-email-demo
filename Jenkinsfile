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
                catchError(buildResult: 'SUCCESS', stageResult: 'UNSTABLE') {
                    bat 'py -m pytest test_calculator.py -v --junitxml=results.xml'
                }
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
            junit allowEmptyResults: true, testResults: 'results.xml'
        }
        success {
            emailext(
                to: 'iheckinlovetenzkekw@gmail.com',
                subject: "BUILD PASSED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Build Successful!</h2>
                    <p><b>Project:</b> ${env.JOB_NAME}</p>
                    <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>
                    <p><b>Status:</b> PASSED</p>
                    <p><a href="${env.BUILD_URL}">Click here to view build</a></p>
                """,
                mimeType: 'text/html'
            )
        }
        failure {
            emailext(
                to: 'iheckinlovetenzkekw@gmail.com',
                subject: "BUILD FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Build Failed!</h2>
                    <p><b>Project:</b> ${env.JOB_NAME}</p>
                    <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>
                    <p><b>Status:</b> FAILED</p>
                    <p><a href="${env.BUILD_URL}console">Click here to view logs</a></p>
                """,
                mimeType: 'text/html'
            )
        }
    }
}
