pipeline {
    agent any

    options {
        skipDefaultCheckout()   // pour éviter le double "Declarative: Checkout SCM"
    }

    tools {
        maven 'Maven-3.9.11'     // ⚠️ même nom que dans "Global Tool Configuration"
    }

    stages {

        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -version'
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
                echo 'Déploiement (placeholder, on branchera Nexus ensuite)...'
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline réussi"
        }
        failure {
            echo "❌ Pipeline échoué"
        }
    }
}
