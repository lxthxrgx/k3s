pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/dotnet/sdk:10.0'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
    stage('Restore') {
            steps {
                sh 'dotnet restore'
            }
        }
        stage('Build') { 
            steps {
                sh 'dotnet restore' 
                sh 'dotnet build --no-restore' 
            }
        }
    }
}