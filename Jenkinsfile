pipeline {
    agent any

    environment {
        PORT = credentials('PORT')
        MONGO_URI = credentials('MONGO_URI')
        JWT_SECRET = credentials('JWT_SECRET')
        JWT_EXPIRES_IN = credentials('JWT_EXPIRES_IN')
    }

    stages {

        stage('Create .env') {
            steps {
                sh '''
                rm -f .env
                echo "PORT=$PORT" > .env
                echo "MONGO_URI=$MONGO_URI" >> .env
                echo "JWT_SECRET=$JWT_SECRET" >> .env
                echo "JWT_EXPIRES_IN=$JWT_EXPIRES_IN" >> .env
                chmod 600 .env
                '''
            }
        }

        stage('Build Docker') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker compose down
                docker compose up -d
                '''
            }
        }

    }
}