pipeline {
    agent {
        docker {
            image 'node:18' // Use your preferred Node.js version
            args '-v $HOME/.npm:/root/.npm' // Optional: cache npm data
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
    }
}
