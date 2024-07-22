pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/ajingliang6268/Vulnerable-Web-Application'
            }
        }
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube';
                    // Print the path of SonarQube scanner
                    sh "echo SonarQube Scanner Path: ${scannerHome}"

                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://192.168.1.89:9000 -Dsonar.token=sqp_b02ee59dce5e6d61d45851531598de3446400748"
                    }
                }
            }
        }
    }
    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}
