pipeline {
    agent any  // Use any available agent
    
    environment {
        SOLUTION_NAME = 'HouseRentingSystem.sln'
        TEST_PROJECT_PATH = 'HouseRentingSystem.UnitTests/HouseRentingSystem.UnitTests.csproj'
    }

    triggers {
        // Poll the repository every minute to check for changes on the 'feature-ci-pipeline' branch
        pollSCM('H/1 * * * *')  // This means Jenkins will check for changes every minute
    }

    options {
        // Stop the build on first failure
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout') {
            when {
                branch 'feature-ci-pipeline'  // Only run when the branch is 'feature-ci-pipeline'
            }
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }

        stage('Build and Test') {
            when {
                branch 'feature-ci-pipeline'  // Only run this stage when the branch is 'feature-ci-pipeline'
            }
            stages {
                stage('Restore Dependencies') {
                    steps {
                        script {
                            // Restore dependencies for the solution
                            bat "dotnet restore ${SOLUTION_NAME}"
                        }
                    }
                }

                stage('Build Solution') {
                    steps {
                        script {
                            // Build the solution in Release mode
                            bat "dotnet build ${SOLUTION_NAME} --configuration Release"
                        }
                    }
                }

                stage('Run Unit Tests') {
                    steps {
                        script {
                            // Run tests from the specific test project
                            bat "dotnet test ${TEST_PROJECT_PATH} --configuration Release --no-build --verbosity normal"
                        }
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
