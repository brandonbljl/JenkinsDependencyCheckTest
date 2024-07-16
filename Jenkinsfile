pipeline {
    agent any

    environment {
        NVD_API_KEY = credentials('nvd-api-key')  // Reference the ID of the credential
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
                dependencyCheck additionalArguments: '--format HTML --format XML --nvdApiKey ${NVD_API_KEY} --nvdApiDelay 2000', 
                odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
            }
        }
    }
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
