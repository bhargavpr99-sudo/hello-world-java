pipeline {
    agent any

    tools {
        jdk 'Java11'
        maven 'Maven3'
    }

    options {
        // Limits the build log size and shows timestamps
        timestamps()
        ansiColor('xterm')
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the repo tied to this pipeline
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Maven build: skip tests, use batch mode, faster logging
                sh 'mvn package -DskipTests --batch-mode'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive all .jar and .war files in target/
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


