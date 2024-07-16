pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'master', 
                url: 'https://github.com/brandonbljl/JenkinsDependencyCheckTest.git'
            }
        }

        stage('OWASP DependencyCheck') {
            steps {
                script {
                    // Execute Dependency Check without NVD updates
                    def scanResultsDir = "${env.WORKSPACE}/dependency-check-results"
                    def reportOutputDir = "${env.WORKSPACE}/dependency-check-reports"

                    sh """
                    dependency-check.sh --scan . \
                    --format HTML --format XML \
                    --noupdate \
                    --out ${scanResultsDir} --format ${reportOutputDir}
                    """
                }
            }
        }
    }

    post {
        success {
            // Publish Dependency Check reports
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: true,
                reportDir: 'dependency-check-reports',
                reportFiles: 'index.html',
                reportName: 'OWASP Dependency Check Report'
            ])
        }
    }
}
