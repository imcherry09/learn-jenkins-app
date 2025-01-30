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
            steps{
                sh '''
                if [-f $WORKSPACE/index.html]; then
                echo "index.html found"
                else 
                echo "Index.html not found"
                npm test
                '''
            }
        }
    }
}