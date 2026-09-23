pipeline {

    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Java application...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Creating JAR file...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Archive') {
            steps {
                echo 'Archiving JAR artifact...'
                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }
    }

    post {

        success {
            echo 'BUILD SUCCESSFUL'
        }

        failure {
            echo 'BUILD FAILED'
        }

        always {
            echo 'Jenkins pipeline completed.'
        }
    }
}
