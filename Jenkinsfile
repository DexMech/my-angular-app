pipeline {
    agent any

    tools {
        nodejs 'node' // Nome configurado no Jenkins
    }

    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    // Garante que o Node.js está instalado

                    sh 'node -v'
                    sh 'npm -v'
                }
                sh 'npm install -g @angular/cli'
                sh 'npm install'
            }
        }

        stage('Run Lint') {
            steps {
                echo 'Running lint checks...'
                sh 'ng lint'
            }
        }

        

        stage('Build Application') {
            steps {
                echo 'Building Angular application...'
                sh 'ng build --configuration production'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
