pipeline {
    agent {
        docker {
            image 'eclipse-temurin:21-jdk'
            args '-v $HOME/.m2:/root/.m2'
        }
    }

    environment {
        MAVEN_OPTS = '-Dmaven.repo.local=$HOME/.m2/repository'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'chmod +x ./mvnw'
                sh './mvnw clean compile -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh './mvnw test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                sh './mvnw package -DskipTests'
            }
        }

        stage('Archive') {
            steps {
                echo 'Archiving artifacts...'
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
        always {
            cleanWs()
        }
    }
}
