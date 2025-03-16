pipeline{
    agent any
    /*
    agent{
        docker{
             image 'node:18-alpine'
             reuseNode true
        }
    }
    */

    stages{  /*
        stage('Build'){
            steps{
                sh '''
                ls -la
                echo "buid started"
                npm install
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

        */
        stage('E2E'){
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }              
            }

            steps{
                sh '''
                npm install -g serve
                sudo serve -s build&
                npm playwright test
                '''
            }
        }
    }

    post{
        always{
            junit "jest-results/junit.xml"
        }
    }
}