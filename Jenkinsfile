pipeline {
    agent any
    environment {
        SOURCE_DIR = "${env.DIRECTORY_PATH ?: 'default/source/path'}"
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
                echo "Building project from source directory: ${SOURCE_DIR}"
                echo "Executing Maven build..."
                // Actual Maven build command can go here
            }
        }
        stage('Testing') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo "Running Unit Tests using JUnit..."
                        // Insert actual JUnit test steps here
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo "Running Integration Tests using Postman..."
                        // Insert actual Postman test steps here
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
                        body: "The unit and integration tests have passed successfully.",
                        to: "pateldhruvi1279@gmail.com",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        subject: "Tests Failed: ${currentBuild.fullDisplayName}",
                        body: "The unit and/or integration tests have failed. Please check the attached logs.",
                        to: "pateldhruvi1279@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
        stage('Code Quality Analysis') {
            steps {
                echo "Performing code quality analysis using SonarQube..."
                // Insert SonarQube analysis steps here
            }
        }
        stage('Security Scanning') {
            steps {
                echo "Conducting security scans using OWASP Dependency-Check..."
                // Insert security scan steps here
            }
            post {
                success {
                    emailext(
                        subject: "Security Scan Successful: ${currentBuild.fullDisplayName}",
                        body: "Security scan completed successfully. Please find the logs attached.",
                        to: "pateldhruvi1279@gmail.com",
                        attachLog: true
                    )
                }
                failure {
                    emailext(
                        subject: "Security Scan Failed: ${currentBuild.fullDisplayName}",
                        body: "Security scan encountered issues. Review the logs for details.",
                        to: "pateldhruvi1279@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to the staging environment..."
                echo "Using AWS for deployment..."
                // Insert AWS deployment steps here
            }
        }
        stage('Staging Integration Tests') {
            steps {
                echo "Executing integration tests on the staging environment..."
                // Insert staging integration test steps here
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to production..."
                echo "Final deployment using AWS..."
                // Insert final production deployment steps here
            }
            post {
                always {
                    echo "Pipeline execution completed."
                    mail to: 'pateldhruvi1279@gmail.com',
                    subject: 'hi',
                    body: 'success'
                }
            }
        }
    }
}
