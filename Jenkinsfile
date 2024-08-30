pipeline {
    agent any
    environment {
        SOURCE_DIR = "${env.DIRECTORY_PATH ?: 'default/source/path'}"
        LOG_FILE = "${env.WORKSPACE}/pipeline.log"
    }
    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code from the repository..."
                // You can add actual checkout steps here if needed, e.g., git checkout
            }
        }
        stage('Build') {
            steps {
                script {
                    sh """
                        echo "Building project from source directory: ${SOURCE_DIR}" | tee -a ${LOG_FILE}
                        echo "Executing Maven build..." | tee -a ${LOG_FILE}
                        # Actual Maven build command can go here, for example:
                        # mvn clean install | tee -a ${LOG_FILE}
                    """
                }
            }
        }
        stage('Testing') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        script {
                            sh """
                                echo "Running Unit Tests using JUnit..." | tee -a ${LOG_FILE}
                                # Insert actual JUnit test steps here
                            """
                        }
                    }
                }
                stage('Integration Tests') {
                    steps {
                        script {
                            sh """
                                echo "Running Integration Tests using Postman..." | tee -a ${LOG_FILE}
                                # Insert actual Postman test steps here
                            """
                        }
                    }
                }
            }
            post {
                always {
                    echo "Tests completed."
                }
                success {
                    emailext(
                        subject: "Tests Passed: ${currentBuild.fullDisplayName}",
                        body: "The unit and integration tests have passed successfully. Logs are attached.",
                        to: "pateldhruvi1279@gmail.com",
                        attachmentsPattern: 'pipeline.log',
                        attachLog: false
                    )
                }
                failure {
                    emailext(
                        subject: "Tests Failed: ${currentBuild.fullDisplayName}",
                        body: "The unit and/or integration tests have failed. Please check the attached logs.",
                        to: "pateldhruvi1279@gmail.com",
                        attachmentsPattern: 'pipeline.log',
                        attachLog: false
                    )
                }
            }
        }
        stage('Code Quality Analysis') {
            steps {
                script {
                    sh """
                        echo "Performing code quality analysis using SonarQube..." | tee -a ${LOG_FILE}
                        # Insert SonarQube analysis steps here
                    """
                }
            }
        }
        stage('Security Scanning') {
            steps {
                script {
                    sh """
                        echo "Conducting security scans using OWASP Dependency-Check..." | tee -a ${LOG_FILE}
                        # Insert security scan steps here
                    """
                }
            }
            post {
                success {
                    emailext(
                        subject: "Security Scan Successful: ${currentBuild.fullDisplayName}",
                        body: "Security scan completed successfully. Please find the logs attached.",
                        to: "pateldhruvi1279@gmail.com",
                        attachmentsPattern: 'pipeline.log',
                        attachLog: false
                    )
                }
                failure {
                    emailext(
                        subject: "Security Scan Failed: ${currentBuild.fullDisplayName}",
                        body: "Security scan encountered issues. Review the logs for details.",
                        to: "pateldhruvi1279@gmail.com",
                        attachmentsPattern: 'pipeline.log',
                        attachLog: false
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    sh """
                        echo "Deploying the application to the staging environment..." | tee -a ${LOG_FILE}
                        echo "Using AWS for deployment..." | tee -a ${LOG_FILE}
                        # Insert AWS deployment steps here
                    """
                }
            }
        }
        stage('Staging Integration Tests') {
            steps {
                script {
                    sh """
                        echo "Executing integration tests on the staging environment..." | tee -a ${LOG_FILE}
                        # Insert staging integration test steps here
                    """
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    sh """
                        echo "Deploying the application to production..." | tee -a ${LOG_FILE}
                        echo "Final deployment using AWS..." | tee -a ${LOG_FILE}
                        # Insert final production deployment steps here
                    """
                }
            }
            post {
                always {
                    echo "Pipeline execution completed."
                    emailext(
                        subject: "Pipeline Completed: ${currentBuild.fullDisplayName}",
                        body: "The pipeline execution has completed. Please find the attached logs.",
                        to: "pateldhruvi1279@gmail.com",
                        attachmentsPattern: 'pipeline.log',
                        attachLog: false
                    )
                }
            }
        }
    }
}
