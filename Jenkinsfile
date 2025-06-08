pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonarqube-token')  // This must exist in Jenkins credentials
    }

    tools {
        sonarQubeScanner 'sonar-scanner'
    }

    stages {
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('LocalSonarQube') {
                    sh """
                        ${tool('sonar-scanner')}/bin/sonar-scanner \
                        -Dsonar.projectKey=microblog \
                        -Dsonar.sources=app \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=${SONAR_TOKEN}
                    """
                }
            }
        }
    }
}