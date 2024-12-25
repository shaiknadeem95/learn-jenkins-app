pipeline {
    agent any

    stages {
        agent{
            docker{
                image 'node:20-alphine'
                reuseNode true
            }
        }
        stage('Build') {
            steps {
                sh ''' 
                 echo "starting the build file"
                 npm ci
                 npm run build
                '''
            }
        }
        stage('Test')
        {
            steps{
                sh '''
                test -f build/index.html
                echo "running the Test case" 
                npm test
                '''
            }
        }
        post {
            always junit 'test-results/junit.xml'
        }
    }
}
