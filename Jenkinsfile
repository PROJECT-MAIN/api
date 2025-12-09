pipeline {
    agent any
    triggers {
        // Déclenche le job à chaque push GitHub (via webhook)
        githubPush()
    }
    stages {
        stage('Build & Deploy to Nexus') {
            steps {
                // Sous Windows : utiliser 'bat'
                bat "mvn clean deploy"
            }
        }
    }
}
