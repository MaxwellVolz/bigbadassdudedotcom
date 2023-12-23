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
                    docker run -d -p 8083:80 -p 8084:443 \
                        -v /etc/letsencrypt/live/bigbadassdude.com/fullchain.pem:/etc/nginx/ssl/fullchain.pem:ro \
                        -v /etc/letsencrypt/live/bigbadassdude.com/privkey.pem:/etc/nginx/ssl/privkey.pem:ro \
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
