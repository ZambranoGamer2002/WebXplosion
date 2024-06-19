pipeline {
    agent any

    environment {
        PHP_VERSION = '7.4' // Cambia a la versión de PHP que estés utilizando
    }

    stages {
        stage('Clonar Repositorio') {
            steps {
                script {
                    // Clonar el repositorio de GitHub
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                        userRemoteConfigs: [[url: 'git@github.com:ZambranoGamer2002/WebXplosion.git',
                                             credentialsId: 'GITHUB']]
                    ])
                }
            }
        }

        stage('Preparar') {
            steps {
                script {
                    // Instalar dependencias utilizando Composer
                    sh 'composer install'
                }
            }
        }

        stage('Ejecutar Pruebas') {
            steps {
                script {
                    // Ejecutar pruebas utilizando PHPUnit
                    sh './vendor/bin/phpunit --configuration phpunit.xml.dist'
                }
            }
        }

        stage('Publicar Resultados') {
            steps {
                // Publicar resultados de pruebas
                junit 'build/logs/logfile.xml'
            }
        }
    }

    post {
        always {
            // Archivar los artefactos siempre
            archiveArtifacts artifacts: 'build/logs/**', allowEmptyArchive: true
        }
        success {
            echo 'La construcción y las pruebas han sido exitosas.'
        }
        failure {
            echo 'La construcción o las pruebas han fallado.'
        }
    }
}
