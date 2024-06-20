pipeline {
    agent any

    stages {
        stage('Preparacion') {
            steps {
                git branch: 'main', url: 'https://github.com/ZambranoGamer2002/WebXplosion.git'
                echo 'Pulled from GitHub successfully'
            }
        }

        stage('Verifica version php') {
            steps {
                sh 'php --version'
            }
        }


        stage('Unit Test php') {
            steps {
                sh 'chmod +x vendor/bin/phpunit'
                sh 'vendor/bin/phpunit'
            }
        }

        // Revisa la calidad de código con SonarQube
        // stage('Sonarqube') {
        //     steps {
        //         script {
        //             def scannerHome = tool name: 'sonarscanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation';
        //             echo "scannerHome = $scannerHome ...."
        //             withSonarQubeEnv() {
        //                 sh "$scannerHome/bin/sonar-scanner"
        //             }
        //         }
        //     }
        // }

        stage('Docker Build') {
            steps {
                sh 'docker build -t simple-php-website .'
            }
        }

        stage('Deploy php') {
            steps {
                sh 'docker compose up -d'
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
