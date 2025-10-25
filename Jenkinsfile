pipeline {
    agent any   // or use label 'windows' if you have a Windows agent

    stages {
        stage('Checkout') {
            when { branch 'feature-ci-pipeline' }
            steps {
                checkout scm
            }
        }

        stage('Restore & Build') {
            when { branch 'feature-ci-pipeline' }
            steps {
                bat 'dotnet restore'
                bat 'dotnet build --no-restore'
            }
        }

        stage('Run All Tests') {
            when { branch 'feature-ci-pipeline' }
            steps {
                echo "Running all tests on feature-ci-pipeline branch..."
                bat 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
