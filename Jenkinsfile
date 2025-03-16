pipeline{
    agent{
        docker{
             image 'node:18-alpine'
             reuseNode true
        }
    }

    stages{
        stage('Build'){
            steps{
                sh '''
                ls -la
                echo "buid started"
                #npm install
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
                echo "Test stage"
                test -f build/index.html
                npm test
                '''
            }  
        }
    }
}