pipeline {
    agent any

    stages {
        stage('Preparacion') {
            steps {
                git 'git@github.com:ZambranoGamer2002/WebXplosion.git'
                echo 'Pulled from GitHub successfully'
            }
        }

        stage('Verifica version php') {
            steps {
                sh 'php --version'
            }
        }

        stage('Instalar dependencias') {
            steps {
                sh 'composer install'
            }
        }

        stage('Ejecutar pruebas') {
            steps {
                sh './vendor/bin/phpunit --configuration phpunit.xml.dist'
            }
        }

        stage('Publicar resultados') {
            steps {
                junit 'build/logs/logfile.xml'
            }
        }
    }

    post {
        always {
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