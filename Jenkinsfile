pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps {
                sh ''' 
                 echo "starting the build file"
                 node --version
                 npm --version
                 npm ci
                 npm run build
                '''
            }
        }
        stage('Test')
        {
            agent{
                docker{
                    image 'node:20-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                test -f build/index.html
                echo "running the Test case" 
                npm test
                '''
            }
        }
    }
    post {
            always {
                junit 'test-results/junit.xml'
            }
    }
}
