pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonarqube-token')  // This must exist in Jenkins credentials
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/jonaytec/microblog.git', branch: 'main'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('LocalSonarQube') {
                    sh """
                    sonar-scanner \
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
