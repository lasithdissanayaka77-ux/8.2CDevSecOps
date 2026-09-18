pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/lasithdissanayaka77-ux/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }

            post {
                success {
                    emailext(
                        to: 'lasithdissanayaka77@gmail.com',
                        subject: "Test Stage - SUCCESS - Build #${BUILD_NUMBER}",
                        body: "The Run Tests stage completed successfully.\n\nProject: ${JOB_NAME}\nBuild: #${BUILD_NUMBER}\nStatus: SUCCESS",
                        attachLog: true
                    )
                }

                failure {
                    emailext(
                        to: 'lasithdissanayaka77@gmail.com',
                        subject: "Test Stage - FAILURE - Build #${BUILD_NUMBER}",
                        body: "The Run Tests stage failed.\n\nProject: ${JOB_NAME}\nBuild: #${BUILD_NUMBER}\nStatus: FAILURE",
                        attachLog: true
                    )
                }
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }

            post {
                success {
                    emailext(
                        to: 'lasithdissanayaka77@gmail.com',
                        subject: "Security Scan - SUCCESS - Build #${BUILD_NUMBER}",
                        body: "The NPM security scan stage completed successfully.\n\nProject: ${JOB_NAME}\nBuild: #${BUILD_NUMBER}\nStatus: SUCCESS",
                        attachLog: true
                    )
                }

                failure {
                    emailext(
                        to: 'lasithdissanayaka77@gmail.com',
                        subject: "Security Scan - FAILURE - Build #${BUILD_NUMBER}",
                        body: "The NPM security scan stage failed.\n\nProject: ${JOB_NAME}\nBuild: #${BUILD_NUMBER}\nStatus: FAILURE",
                        attachLog: true
                    )
                }
            }
        }
    }
}
