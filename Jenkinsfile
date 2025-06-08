pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonarqube-token') // ID of your Jenkins secret text credential
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/jonaytec/microblog.git'
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
                        -Dsonar.login=$SONAR_TOKEN
                    """
                }
            }
        }
    }
}
