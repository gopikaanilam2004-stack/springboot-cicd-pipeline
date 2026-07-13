pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven3'
    }

    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        timestamps()
    }

    stages {

        stage('Verify Environment') {
            steps {
                sh '''
                    echo "Java Version:"
                    java -version

                    echo "Maven Version:"
                    mvn -version
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Building Spring Boot application...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo 'Running SonarQube Code Analysis...'

                withSonarQubeEnv('SonarQube') {
                    sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=health-monitor \
                    -Dsonar.projectName=health-monitor
                    '''
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {

        success {
            echo 'BUILD SUCCESS'
        }

        failure {
            echo 'BUILD FAILED'
        }

        always {
            echo 'Pipeline completed'
        }
    }
}
