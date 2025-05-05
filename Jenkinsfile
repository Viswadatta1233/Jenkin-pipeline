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
                // Check if index.html exists
                sh '''
                    if [ -f build/index.html ]; then
                        echo "index.html exists in build directory."
                    else
                        echo "index.html is missing!"
                        exit 1
                    fi
                '''
                
                // Run tests (assumes test reporter is configured)
                sh 'npm test'
            }
            post {
                always {
                   junit 'test-results/junit.xml'

                }
            }
        }
    }
}
