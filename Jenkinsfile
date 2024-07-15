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
                        '--nvdApiDelay', '3000'
                    ].join(' ')
                    dependencyCheck additionalArguments: additionalArgs, odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                }
            }
        }
    }
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
