pipeline {


    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18'
                    args '-v $HOME/.npm:/root/.npm'
                    reuseNode true
                }
            }
            steps {
                sh 'npm ci'
                sh 'npm run build'
            }
        }

        stage('Test') {
            agent {
                docker {
                    image 'node:18'
                    args '-v $HOME/.npm:/root/.npm'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    if [ -f build/index.html ]; then
                        echo "index.html exists in build directory."
                    else
                        echo "index.html is missing!"
                        exit 1
                    fi
                '''
                sh 'npm test'
            }
        }

        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
             
                    npm install serve
                    node_modules/.bin/serve -s build &

                    sleep 10

                    
                    npx playwright test
                '''
            }
        }
    }

    post {
        always {
            junit 'jest-results/junit.xml'
        }
    }
}
