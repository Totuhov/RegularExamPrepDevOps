pipeline {
    agent any

    triggers {
        pollSCM('H/1 * * * *')  // Poll the SCM every minute to check for changes
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out the code from the repository
                checkout scm
            }
        }

        stage('Build and Test') {
            // when {
            //     branch 'feature-ci-pipeline'  // Run only on the 'feature-ci-pipeline' branch
            // }
            stages {
                stage('Chechout branch'){
                    steps{
                        bat "git checkout feature-ci-pipeline"
                    }
                }
                stage('Restore Dependencies') {
                    steps {
                        bat "dotnet restore"  // Restore dependencies for the solution
                    }
                }

                stage('Build Solution') {
                    steps {
                        bat "dotnet build"  // Build the solution
                    }
                }

                stage('Run Unit Tests') {
                    steps {
                        bat "dotnet test --no-build --verbosity normal"  // Run tests without building again
                    }
                }
            }
        }
    }
}
