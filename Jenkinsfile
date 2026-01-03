pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "hardik/email-notification:v1"
        EMAIL_TO = "hardikaws@yopmail.com"   // Change to your email
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/hardiksharma1998/email-notification-devops.git'
            }
        }
    }

    post {
        success {
            emailext(
                to: "${EMAIL_TO}",
                subject: "✅ SUCCESS: Jenkins Job ${env.JOB_NAME} Build ${env.BUILD_NUMBER}",
                body: """\
Build SUCCESS!
Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}
"""
            )
        }

        failure {
            emailext(
                to: "${EMAIL_TO}",
                subject: "❌ FAILURE: Jenkins Job ${env.JOB_NAME} Build ${env.BUILD_NUMBER}",
                body: """\
Build FAILED!
Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}
"""
            )
        }

        unstable {
            emailext(
                to: "${EMAIL_TO}",
                subject: "⚠️ UNSTABLE: Jenkins Job ${env.JOB_NAME} Build ${env.BUILD_NUMBER}",
                body: """\
Build is UNSTABLE!
Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}
"""
            )
        }
    }
}
