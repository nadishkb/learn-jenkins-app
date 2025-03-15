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
                echo "buid started"
                npm --version
                npm run build
                '''
            }

                

            
        }
    }
}