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
                dependencyCheck additionalArguments: '--format HTML --format XML --nvdApiKey 995b7b5f-59e3-4685-a180-17c9aca2fa80', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
            }
        }
    }
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
