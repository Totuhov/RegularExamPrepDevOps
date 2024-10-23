pipeline {
    agent any 
    triggers {
        pollSCM('H/1 * * * *')
    }
    stages {
        stage('Checkout') {
            when {
                branch 'dfeature-ci-pipeline '  // Only run when the branch is 'feature-ci-pipeline '
            }
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }

        stage('Build and Test') {
            when {
                branch 'feature-ci-pipeline '  // Only run this stage when the branch is 'feature-ci-pipeline '
            }
            stages {
                stage('Restore Dependencies') {
                    steps {
                        script {
                            // Restore dependencies for the solution
                            bat "dotnet restore"
                        }
                    }
                }

                stage('Build Solution') {
                    steps {
                        script {
                            // Build the solution in Release mode
                            bat "dotnet build"
                        }
                    }
                }

                stage('Run Unit Tests') {
                    steps {
                        script {
                            // Run tests from the specific test project
                            bat "dotnet test --no-build --verbosity normal"
                        }
                    }
                }
            }
        }
    }
}