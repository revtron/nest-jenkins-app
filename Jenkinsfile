pipeline {
    agent any

    environment {
        APP_NAME = "nest-jenkins-app"
        APP_DIR = "/var/www/nest-jenkins-app"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'git@github.com:revtron/nest-jenkins-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                  rsync -av --delete ./ $APP_DIR
                  cd $APP_DIR
                  pm2 delete $APP_NAME || true
                  pm2 start dist/main.js --name $APP_NAME
                  pm2 save
                '''
            }
        }
    }
}


































