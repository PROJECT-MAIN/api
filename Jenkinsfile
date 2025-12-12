pipeline {
    agent any

    stages {

        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo Déploiement en cours...'
            }
        }
    }

    post {
        success {
            echo "✔ Pipeline OK"
        }
        failure {
            echo "❌ Pipeline échoué"
        }
    }
}
