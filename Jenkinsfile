pipeline {
    agent any
    stages {
        stage('Debug') {
            steps {
                echo 'Starting pipeline execution...'
                sh 'env'
            }
        }
        stage('Check Environment') {
            steps {
                echo 'Checking Environment...'
                sh 'docker ps'
            }
        }
        stage('Build and Deploy Intervolz Locally') {
            steps {
                sh '''
                    docker build -t bigbadassdude-website .
                    docker stop bigbadassdude-website-container || true
                    docker rm bigbadassdude-website-container || true
                    docker run -d \
                        --network intervolz-network \
                        -v /etc/letsencrypt/live/bigbadassdude.com/fullchain.pem:/etc/nginx/ssl/fullchain2.pem:ro \
                        -v /etc/letsencrypt/live/bigbadassdude.com/privkey.pem:/etc/nginx/ssl/privkey2.pem:ro \
                        --name bigbadassdude-website-container bigbadassdude-website
                '''
            }
        }
        stage('Celebrate good times!') {
            steps {
                echo 'We are celebrating...'
            }
        }
    }
}
