pipeline {
    agent any

    stages {
        stage('Preparacion') {
            steps {
                git branch: 'main', url: 'git@github.com:ZambranoGamer2002/WebXplosion.git'
                echo 'Pulled from GitHub successfully'
            }
        }

        stage('Verifica version php') {
            steps {
                sh 'php --version'
            }
        }

        stage('Unit Test php'){
            steps {
                //sh 'chmod 0775 vendor/bin/phpunit'
                sh 'chmod +x vendor/bin/phpunit'
                sh 'vendor/bin/phpunit'
            }
        }

       stage('Verifica version php'){
            steps {
                sh 'php --version'
            }
        }

        stage('Unit Test php'){
            steps {
                //sh 'chmod 0775 vendor/bin/phpunit'
                sh 'chmod +x vendor/bin/phpunit'
                sh 'vendor/bin/phpunit'
            }
        }
         //Revisa la calidad de código con SonarQube
        //stage ('Sonarqube') {
        //    steps {
        //        script {
        //            def scannerHome = tool name: 'sonarscanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation';
        //            echo "scannerHome = $scannerHome ...."
        //            withSonarQubeEnv() {
        //                sh "$scannerHome/bin/sonar-scanner"
        //            }
        //        }
        //    }
        //}

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
}
