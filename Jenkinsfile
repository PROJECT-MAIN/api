pipeline {
    agent any

    options {
        // On désactive le checkout automatique implicite
        skipDefaultCheckout()
    }

    tools {
        // Doit correspondre au nom configuré dans "Global Tool Configuration"
        maven 'Maven-3.9.9'
    }

    environment {
        // Lie le credential 'nexus-jenkins' à la variable NEXUS
        // Jenkins crée automatiquement :
        //   NEXUS_USR = username
        //   NEXUS_PSW = password
        NEXUS = credentials('nexus-jenkins')
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -s settings.xml clean package -DskipTests'
            }
        }

        stage('Tests') {
            steps {
                // tu peux séparer les tests unitaires ici si tu veux
                sh 'mvn -s settings.xml test'
            }
        }

        stage('Deploy to Nexus') {
            when {
                // Optionnel : ne déployer que sur certaines branches
                anyOf {
                    branch 'release/1.0.0'
                    branch 'master'
                    branch 'main'
                }
            }
            steps {
                // Déploiement : Maven va utiliser distributionManagement + settings.xml
                sh 'mvn -s settings.xml deploy -DskipTests=true'
            }
        }
    }

    post {
        success {
            echo "✅ Build + Tests + Deploy OK pour la branche ${env.BRANCH_NAME}"
        }
        failure {
            echo "❌ Pipeline échoué sur la branche ${env.BRANCH_NAME}"
        }
    }
}
