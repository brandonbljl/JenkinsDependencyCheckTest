pipeline {
    agent any
    
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('OWASP DependencyCheck') {
            steps {
                script {
                    def additionalArgs = [
                        '--format', 'HTML',
                        '--format', 'XML',
                        '--nvdApiKey', '995b7b5f-59e3-4685-a180-17c9aca2fa80',
                        '--nvdApiDelay', '5000' // 5 seconds delay between API calls
                    ].join(' ')
                    
                    retry(5) {
                        // Retry block for handling transient errors
                        try {
                            dependencyCheck additionalArguments: additionalArgs,
                                            odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                        } catch (Exception e) {
                            echo "Failed to execute dependencyCheck: ${e.message}"
                            throw e
                        }
                    }
                }
            }
        }
    }
    
    post {
        success {
            // Publisher step for successful builds
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
