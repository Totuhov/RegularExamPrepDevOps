pipeline {
    agent any  // Use any available agent
    
    stages {

        stage('Build and Test') {
            stages {
                stage('Restore Dependencies') {
                    steps {
                        script {
                            // Restore dependencies for the solution
                            bat "dotnet restore "
                        }
                    }
                }

                stage('Build Solution') {
                    steps {
                        script {
                            // Build the solution in Release mode
                            bat "dotnet build "
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
