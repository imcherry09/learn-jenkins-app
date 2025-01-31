pipeline{
    agent any
    stages{
        stage('Build'){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                node --version
                npm --version 
                npm ci
                npm run build
                '''
            }
        }
        stage('Test'){
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                echo "Test Stage"
                test -f build/index.html
                npm test
                '''
            }
        }
        stage('E2E'){
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.50.0-jammy'
                    reuseNode true
                    
                }
            }
            steps{
                unstash 'build-files'
        sh '''
        npm install serve
        nohup node_modules/.bin/serve -s build > serve.log 2>&1 &
        sleep 10
        npm ci
        PLAYWRIGHT_BROWSERS_PATH=0 npx playwright install --with-deps
        npx playwright test --reporter=html
        '''
            }
        }
    }
    post{
        always{
            junit 'jest-results/junit.xml'
        }
    }
}