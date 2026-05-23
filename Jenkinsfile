pipeline {
    agent any

    environment {
        PROJECT_PATH = "C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\MyApp-CICD"
        PUBLISH_PATH = "C:\\publish"
        IIS_PATH = "C:\\inetpub\\MyApp"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/gouseshake0786/hello-docker.git'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet restore'
                bat 'dotnet build --configuration Release'
            }
        }

        stage('Publish') {
            steps {
                bat 'dotnet publish -c Release -o C:\\publish'
            }
        }

        stage('Deploy to IIS') {
            steps {

                bat '''
                xcopy /E /Y /I C:\\publish\\* C:\\inetpub\\MyApp\\
                '''

            }
        }

        stage('Restart IIS') {
            steps {
                bat 'iisreset'
            }
        }
    }
}
