pipeline {
    agent any

    tools {
        jdk 'Java11'
        maven 'Maven3'
    }

    options {
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn package -DskipTests --batch-mode'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar, target/*.war', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build & Artifact Archiving Successful ✅"
        }
        failure {
            echo "Build Failed ❌"
        }
    }
}
