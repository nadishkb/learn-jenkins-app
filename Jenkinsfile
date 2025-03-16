pipeline{
    agent any

    stages{
        stage('Build'){
            agent{
                 docker{
                     image 'node:18-alpine'
                     reuseNode true
                }
            }
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
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
    
            steps{
                sh '''
                echo "Test stage"
                test -f build/index.html
                npm test
                '''
            }  
        }

    
        stage('E2E'){
            agent{
                docker{
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }              
            }

            steps{
                sh '''
                npm install serve
                node_modules/.bin/serve -s build&
                sleep 5
                #npx playwright test
                npx playwright test --reporter=html
                '''
            }
        }
    }

    post{
        always{
            junit "jest-results/junit.xml"
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, icon: '', keepAll: false, reportDir: 'playwright-report', reportFiles: 'index.html', reportName: 'npx HTML Report', reportTitles: '', useWrapperFileDirectly: true])
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, icon: '', keepAll: false, reportDir: 'jest-results', reportFiles: 'junit.xml', reportName: 'XML Report', reportTitles: '', useWrapperFileDirectly: true])
        }
    }
}