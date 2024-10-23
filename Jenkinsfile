pipeline {
    agent any

    triggers {
        pollSCM('H/3 * * * *')  // Poll the SCM every minute to check for changes
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out the code from the repository
                checkout scm
            }
        }
        stage('Restore Dependencies') {
            steps {
                script {
                    bat "dotnet restore"  // Restore dependencies for the solution
                }
            }
        }
        stage('Build Solution') {
            steps {
                script {
                    bat "dotnet build"  // Build the solution
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    bat "dotnet test --no-build --verbosity normal"  // Run tests without building again
                }
            }
        }
    }
}
