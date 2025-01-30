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
                ls -la
                node --version
                npm --version 
                npm ci
                npm run build
                ls -la
                '''
            }
        }
        stage('Test'){
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }
            steps{
                sh '''
                echo "Test Stage"
                if [-f $WORKSPACE/index.html]; then
                echo "index.html found"
                else 
                echo "index.html not found"
                fi
                npm test
                '''
            }
        }
    }
}