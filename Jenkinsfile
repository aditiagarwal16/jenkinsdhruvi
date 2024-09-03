pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Starting the build process by fetching source code from ${env.DIRECTORY_PATH}"
                echo "Compiling the source code and generating required artifacts"
                echo "Using Maven for build automation"
            }
        }

        stage('Testing - Unit and Integration') {
            steps {
                echo "Executing Unit Tests"
                echo "Running Integration Tests"
                echo "Utilizing JUnit for Unit Testing and Postman for Integration Testing"
            }
            post {
                success {
                    emailext body: "Unit and Integration Tests passed successfully. Please find the attached test logs.",
                             to: 'pateldhruvi1279@gmail.com',
                             subject: "Success: Unit and Integration Tests",
                             attachmentsPattern: 'test.log',
                             attachLog: true
                }
                failure {
                    emailext body: "Unit and Integration Tests failed. Attached are the test logs.",
                             to: 'pateldhruvi1279@gmail.com',
                             subject: "Failure: Unit and Integration Tests",
                             attachmentsPattern: 'test.log',
                             attachLog: true
                }
            }
        }

        stage('Code Quality Analysis') {
            steps {
                echo "Running Code Analysis"
                echo "Using SonarQube Scanner for Jenkins"
            }
        }

        stage('Security Vulnerability Scan') {
            steps {
                echo "Performing security vulnerability scan"
                echo "Using OWASP Dependency-Check plugin"
            }
            post {
                success {
                    emailext body: "Security Scan completed successfully. Please find the attached logs.",
                             to: 'pateldhruvi1279@gmail.com',
                             subject: "Success: Security Scan",
                             attachmentsPattern: 'test.log',
                             attachLog: true
                }
                failure {
                    emailext body: "Security Scan failed. Attached are the logs.",
                             to: 'pateldhruvi1279@gmail.com',
                             subject: "Failure: Security Scan",
                             attachmentsPattern: 'test.log',
                             attachLog: true
                }
            }
        }

        stage('Staging Deployment') {
            steps {
                echo "Deploying the application to the staging environment"
                echo "Using AWS for deployment"
            }
        }

        stage('Staging Environment Tests') {
            steps {
                echo "Executing integration tests on the staging environment"
                echo "Using JUnit for testing"
            }
        }

        stage('Production Deployment') {
            steps {
                echo "Deploying the application to the production environment"
                echo "Utilizing AWS for deployment"
            }
        }
    }
}
