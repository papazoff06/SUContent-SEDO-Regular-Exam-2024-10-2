pipeline {
    agent {
        label 'windows'   // Ensure this runs on a Windows Jenkins agent
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore & Build') {
            steps {
                bat 'dotnet restore'
                bat 'dotnet build --no-restore'
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'develop') {
                        echo "Running Unit Tests Only..."
                        bat 'dotnet test --no-build --filter TestCategory=Unit'
                    } 
                    else if (env.BRANCH_NAME == 'staging') {
                        echo "Running Integration Tests Only..."
                        bat 'dotnet test --no-build --filter TestCategory=Integration'
                    }
                    else if (env.BRANCH_NAME == 'feature-ci-pipeline') {
                        echo "Running All Tests..."
                        bat 'dotnet test --no-build --verbosity normal'
                    } 
                    else {
                        echo "No tests configured for this branch."
                    }
                }
            }
        }
    }
}
