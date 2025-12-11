pipeline {
    agent any          // exécute sur n'importe quel agent disponible

    // 👉 Trigger : le pipeline se lance à chaque push GitHub
    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Récupération du code depuis GitHub"
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Étape de build (à adapter)"
                // Exemple :
                // sh 'mvn clean package'
                // ou
                // sh 'npm install && npm test'
            }
        }

        stage('Tests') {
            steps {
                echo "Étape de tests (à adapter)"
                // Exemple :
                // sh 'mvn test'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'   // exécute ce stage seulement sur la branche main
            }
            steps {
                echo "Déploiement (à définir selon ton besoin)"
            }
        }
    }
}
