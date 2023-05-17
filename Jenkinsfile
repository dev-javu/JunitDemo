pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
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
                // Construye tu proyecto Spring Boot utilizando Gradle
                sh './gradlew clean build'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Realiza el análisis del proyecto con SonarQube Scanner
                // Asegúrate de tener instalado el plugin SonarQube Scanner en Jenkins
                withSonarQubeEnv('SonarCloud') {
                    // Configura las propiedades específicas de SonarQube para el proyecto
                    // Puedes personalizarlas según tus necesidades
                    def sonarqubeProperties = [
                        '-Dsonar.projectKey=walgomwizeline_JunitDemo',
                        '-Dsonar.organization=walgomwizeline',
                        '-Dsonar.sources=src/main',
                        '-Dsonar.tests=src/test',
                        '-Dsonar.java.binaries=build/classes/java/main',
                        '-Dsonar.java.test.binaries=build/classes/java/test'
                    ]
                    sh "./gradlew sonarqube ${sonarqubeProperties.join(' ')}"
                }
            }
        }
    }
}