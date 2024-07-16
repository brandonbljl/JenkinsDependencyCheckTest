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
                dependencyCheck additionalArguments: '--format HTML --format XML', odcInstallation: 'OWASP_Dependency-Check_Vulnerabilities'
            }
        }
    }

    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
