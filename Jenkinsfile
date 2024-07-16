pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                // Checkout the Git repository
                git branch: 'master', url: 'https://github.com/brandonbljl/JenkinsDependencyCheckTest.git'
            }
        }

        stage('OWASP DependencyCheck') {
            steps {
                // Run OWASP DependencyCheck with specified options
                dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'Default'
            }
        }
    }

    post {
        success {
            // Publish DependencyCheck reports
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
