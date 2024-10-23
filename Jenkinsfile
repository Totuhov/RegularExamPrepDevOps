pipeline {
    agent any 
    stages {
	stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout feature-ci-pipeline
            }
        }
    stage('Build and Test') {
        when {
                    branch 'develop'  // Runs only if the branch is 'develop'
                }
            stages {
                    stage('Restore Dependencies') { 
                        steps {
                        bat "dotnet restore"
                        }
                }
                stage('Build Solution') { 
                    steps {
                        bat "dotnet build --no-restore "
                    }
                }
                stage('Deploy') { 
                    steps {
                        bat "dotnet test --no-build"
                    }
                }
            }
        }
    }
}
