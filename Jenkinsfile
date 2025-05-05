pipeline {
    agent {
        docker {
            image 'node:18'
            args '-v $HOME/.npm:/root/.npm'
            reuseNode true
        }
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm ci'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                echo 'Test stage'
            }
        }
    }
}
