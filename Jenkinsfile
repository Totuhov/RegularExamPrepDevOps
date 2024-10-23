pipeline {
    agent any 
    triggers {
        pollSCM('H/1 * * * *')
    }
    stages {
         when {
                branch 'feature-ci-pipeline'
            }
            stages {
                stage('Restore Dependencies') {
                    steps {
                        script {
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
                            bat "dotnet test -no-build --verbosity normal"
                        }
                    }
                }
            }
    }
}