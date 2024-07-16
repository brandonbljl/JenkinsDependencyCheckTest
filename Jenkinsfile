pipeline {
    agent any
    environment {
        NVD_API_KEY = credentials('nvd-api-key')
    }
    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'master', 
                url: 'https://github.com/brandonbljl/JenkinsDependencyCheckTest.git',
                credentialsId: 'jenkins-PAT'
            }
        }

        stage('OWASP DependencyCheck') {
            steps {
                dependencyCheck additionalArguments: '--format HTML --format XML', 
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


// curl -H "Accept: application/json" -H "apiKey: daa2a872-5f39-404c-bbec-578bb5b7f61d" -v https://services.nvd.nist.gov/rest/json/cves/2.0\?cpeName\=cpe:2.3:o:microsoft:windows_10:1607:\*:\*:\*:\*:\*:\*:\*