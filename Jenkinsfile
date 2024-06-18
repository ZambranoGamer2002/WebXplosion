pipeline {
    agent any

    stages {
        stage('Preparacion') {
            steps {
                git 'git@github.com:ZambranoGamer2002/WebXplosion.git'
                echo "Pulled from GitHub successfully"
            }
        }

        stage('Verifica version php') {
            steps {
                sh 'php --version'
            }
        }

        stage('Ejecutar php') {
            steps {
                sh 'php index.php'
            }
        }

        //Revisa la calidad de codigo con SonarQube
        //stage ('SonarQube') {
        //    steps {
        //        script {
        //            def scannerHome = tool name: 'sonarscanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation';
        //            echo "scannerHome = $scannerHome ......."
        //            withSonarQubeEnv() {
        //                sh "$scannerHome/bin/sonar-scanner"
        //            }
        //        }
        //    }
        //}
    }
}