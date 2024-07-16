pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'master', url: 'https://github.com/brandonbljl/JenkinsDependencyCheckTest.git'
            }
        }

        stage('OWASP DependencyCheck') {
            steps {
                dependencyCheck additionalArguments: '--format HTML --format XML --nvdApiKey df7daa95-6d20-4f57-8f00-5496ad92b9d9 --nvdApiDelay 15000 --nvdApiRetries 3', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
            }
        }
    }

    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
