pipeline {
    agent any

    environment {
        CHECKMARX_SKIP_SCAN = "${env.CHECKMARX_SKIP_SCAN ?: 'false'}"
    }

    stages {
        stage('Check Scan Status') {
            steps {
                script {
                    def skipScan = env.CHECKMARX_SKIP_SCAN.toLowerCase() == 'true'
                    def runCheckmarx = !skipScan
                    echo "🔍 Checkmarx status: ${runCheckmarx ? 'ENABLED' : 'SKIPPED'}"
                    
                    // Save for later stages
                    env.RUN_CHECKMARX = runCheckmarx.toString()
                }
            }
        }

        stage('Run Checkmarx') {
            when {
                expression { return env.RUN_CHECKMARX == 'true' }
            }
            steps {
                echo "✅ Running Checkmarx scan..."
                // Add actual scan logic here
            }
        }

        stage('Build') {
            steps {
                echo "🚀 Build logic continues regardless of Checkmarx..."
            }
        }
    }
}
