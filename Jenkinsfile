pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven'
    }

    options {
        buildDiscarder(logRotator(
            numToKeepStr: '5'
        ))
        timestamps()
    }

    stages {

        stage('Verify Environment') {
            steps {
                sh '''
                echo "Checking Java version"
                java -version

                echo "Checking Maven version"
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

        stage('Archive Artifact') {
            steps {
                echo 'Archiving JAR file...'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

    }

    post {

        success {
            echo '✅ Build completed successfully!'
        }

        failure {
            echo '❌ Build failed. Check console output.'
        }

        always {
            echo 'Pipeline execution completed.'
        }
    }
}}
