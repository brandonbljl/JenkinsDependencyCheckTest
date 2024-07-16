pipeline {
    agent any

    environment {
        SCAN_RESULTS_DIR = "${WORKSPACE}/dependency-check-results"
        REPORT_OUTPUT_DIR = "${WORKSPACE}/dependency-check-reports"
    }

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
                    // Ensure Dependency Check tool is available
                    def dependencyCheckHome = tool name: 'OWASP_Dependency-Check_Vulnerabilities', type: 'org.jenkinsci.plugins.tools.ToolInstallation'
                    def dependencyCheckScript = "${dependencyCheckHome}/bin/dependency-check.sh"

                    // Execute Dependency Check scan
                    sh """
                    ${dependencyCheckScript} --scan . \
                    --format HTML --format XML \
                    --noupdate \
                    --out ${SCAN_RESULTS_DIR} --format ${REPORT_OUTPUT_DIR}
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
