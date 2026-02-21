pipeline {
    agent { label 'windows' }
    stages {
        stage('Restore dependencies') {
            when {
                anyOf {
                    branch 'main'
                    branch 'feature'
                }
            }
            steps {
                bat 'dotnet restore SoftUniBazar.sln'
            }
        }
        stage('Build the app') {
            when {
                anyOf {
                    branch 'main'
                    branch 'feature'
                }
            }
            steps {
                bat 'dotnet build SoftUniBazar.sln --no-restore'
            }
        }
        stage('Run tests') {
            when {
                anyOf {
                    branch 'main'
                    branch 'feature'
                }
            }
            steps {
                bat 'dotnet test SoftUniBazar.sln --no-build --verbosity normal --logger trx --results-directory TestResults'
            }
        }
        stage('Skip non-target branches') {
            when {
                not {
                    anyOf {
                        branch 'main'
                        branch 'feature'
                    }
                }
            }
            steps {
                echo "Skipping branch '${env.BRANCH_NAME}'. This multibranch pipeline only runs for 'main' and 'feature'."
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'TestResults/**/*.trx', allowEmptyArchive: true
        }
    }
}
