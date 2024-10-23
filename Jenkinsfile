pipeline {
    agent any 
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
        stage('Run Tests') { 
            steps {
                bat "dotnet test --no-build"
            }
        }
    }
}