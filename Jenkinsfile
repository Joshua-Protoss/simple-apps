pipeline {
    agent {label 'devops1-biawak'}
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Joshua-Protoss/simple-apps.git'
            }
        }
        stage('Build') {
            steps {
                sh ''' cd app
                npm install '''
            }
        }
        
        stage('Testing App') {
            steps {
                sh ''' cd app
                npm test
                npm run test:coverage '''
            }
        }
        stage('Code Analysis') {
            steps {
                sh ''' cd app
                sonar-scanner \
                    -Dsonar.projectKey=simple-apps \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://172.23.8.77:9000 \
                    -Dsonar.token=sqp_0f8e54373f39bc89210b59e4c3b9930a8774c76b '''
            }
        }
        stage('Deploy App') {
            steps {
                sh ''' 
                docker compose build
                docker compose up -d '''
            }
        }
    }
}