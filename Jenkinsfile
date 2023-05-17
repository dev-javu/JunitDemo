pipeline {
    agent any

    environment {
        SONAR_HOST_URL = "https://sonarcloud.io"
        SONAR_TOKEN = credentials('233b4df0667171194f7382fc37bc0b9ea2b7780f')
    }

    stages {
        stage('Checkout') {
            steps {
                // Realiza la clonación del repositorio o la obtención del código fuente del proyecto
                // Puedes utilizar el paso 'checkout' para proyectos de Git
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Construye tu proyecto Java utilizando Gradle
                sh './gradlew clean build'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Realiza el análisis del proyecto con SonarQube Scanner
                // Asegúrate de tener instalado el plugin SonarQube Scanner en Jenkins
                withSonarQubeEnv('SonarCloud') {
                    sh './gradlew sonarqube'
                }
            }
        }
    }
}