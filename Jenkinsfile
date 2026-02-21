pipeline {
    agent any

    stages {
        stage("Restore dependencies") {
            when {
                anyOf {
                    branch 'main'
                    expression { env.BRANCH_NAME?.startsWith('feature') }
                }
            }
            steps {
                sh 'dotnet restore'
            }
        }

        stage("Build the app") {
            when {
                anyOf {
                    branch 'main'
                    expression { env.BRANCH_NAME?.startsWith('feature') }
                }
            }
            steps {
                sh 'dotnet build --no-restore'
            }
        }

        stage("Run the tests") {
            when {
                anyOf {
                    branch 'main'
                    expression { env.BRANCH_NAME?.startsWith('feature') }
                }
            }
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}