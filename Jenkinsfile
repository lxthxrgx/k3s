pipeline {
    // Defines where the pipeline will run. 'any' means any available agent.
     agent {
        docker {
            image 'mcr.microsoft.com/dotnet/sdk:8.0'
        }
    }
    // Stages define the main steps of the CI process
    stages {
        stage('Restore Dependencies') {
            steps {
                // Restore NuGet dependencies
                sh 'dotnet restore'
            }
        }
        stage('Build') {
            steps {
                // Build the application in Release mode
                sh 'dotnet build --configuration Release --no-restore'
            }
        }
        stage('Test') {
            steps {
                // Run unit tests (assumes a test project exists in the solution)
                sh 'dotnet test --configuration Release --no-build --verbosity normal'
            }
        }
        stage('Publish') {
            steps {
                // Publish the application to a 'publish_output' directory
                sh 'dotnet publish --configuration Release --no-build --output ./publish_output'
                // Archive the published artifacts
                archiveArtifacts artifacts: 'publish_output/**'
            }
        }
    }
}
