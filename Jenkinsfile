pipeline {
    agent any

    environment {
        ALERT_EMAIL = 'alynalakhani431@gmail.com'
    }

    parameters {
        choice(name: 'OUTCOME', choices: ['success', 'failure', 'unstable'], description: 'Choose the build result to simulate')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building Community Services Management System...'
            }
        }
        stage('Test') {
            steps {
                script {
                    if (params.OUTCOME == 'failure') {
                        error('Simulated test failure')
                    } else if (params.OUTCOME == 'unstable') {
                        unstable('Simulated unstable build')
                    } else {
                        echo 'All tests passed'
                    }
                }
            }
        }
    }

    post {
        success {
            mail to: "${env.ALERT_EMAIL}",
                 subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build succeeded.\nDetails: ${env.BUILD_URL}"
        }
        failure {
            mail to: "${env.ALERT_EMAIL}",
                 subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build failed. Please check the console output.\nDetails: ${env.BUILD_URL}"
        }
        unstable {
            mail to: "${env.ALERT_EMAIL}",
                 subject: "UNSTABLE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "The build is unstable. Some checks did not pass.\nDetails: ${env.BUILD_URL}"
        }
    }
}
