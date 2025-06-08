pipeline {
    agent any

    tools {
        // No need for jdk or nodejs in this case
        // Only SonarQube Scanner is required
        sonarRunner 'Default'
    }

    environment {
        SCANNER_HOME = tool 'Default'
        SONAR_TOKEN = credentials('sonarqube-token')
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/jonaytec/microblog.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('LocalSonarQube') {
                    sh '''
                        $SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.projectKey=microblog \
                        -Dsonar.sources=app \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
    }
}

