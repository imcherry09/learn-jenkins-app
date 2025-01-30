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
                found_file=$(find "$WORKSPACE" -type f -name "index.html" | head -n 1)
                if [-n $found_file]; then
                echo "index.html found at" 
                echo "$found_file"
                else 
                echo "index.html not found"
                exit 1
                fi
                npm test
                '''
            }
        }
    }
}