pipeline {
    agent any
    

    triggers {
        pollSCM('H/1 * * * *')
    }

    stages {        
        stage('Build and Test') {
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
                            bat "dotnet build"
                        }
                    }
                }

                stage('Run Unit Tests') {
                    steps {
                        script {
                            bat "dotnet test --no-build --verbosity normal"
                        }
                    }
                }
            }
        }
    }
}
