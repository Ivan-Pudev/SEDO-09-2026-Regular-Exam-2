
pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                sh 'dotnet restore Homies.sln'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build Homies.sln --configuration Release --no-restore'
            }
        }

        stage('Run All Tests') {
            steps {
                sh 'dotnet test Homies.sln --configuration Release --no-build --no-restore --logger "console;verbosity=normal"'
            }
        }
    }

    post {
        always {
            echo 'Jenkins pipeline finished.'
        }
        success {
            echo 'Build and tests passed.'
        }
        failure {
            echo 'Build or tests failed. Check the console output.'
        }
    }
}
