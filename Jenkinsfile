pipeline {
    agent any

    tools {
        nodejs 'node' // Nome configurado no Jenkins
    }

    environment {
        GITHUB_TOKEN = credentials('segredocoisado') // ID da credencial
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

        stage('Deploy to GitHub Pages') {
                steps {
                    timeout(time: 1, unit: 'MINUTES') {
                        sh 'git config --global user.email "alex.junior.carlos23@gmail.com"'
                        sh 'git config --global user.name "alex.silva"'
                        sh 'git remote set-url origin https://${GITHUB_TOKEN}@github.com/dexmech/my-angular-app.git'
                        sh 'ng deploy --base-href=/my-angular-app/ --no-silent'
                }
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
