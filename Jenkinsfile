pipeline {
    agent any

    environment {
        APP_NAME = "nest-jenkins-app"
        APP_DIR = "/var/www/nest-jenkins-app"
    }

    stages {

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
                  rsync -av ./ $APP_DIR
                  cd $APP_DIR
                  npm install
                  npm run build
                  pm2 delete nest-jenkins-app || true
                  pm2 start dist/main.js --name nest-jenkins-app
                  pm2 save
                '''
            }
        }
    }
}

