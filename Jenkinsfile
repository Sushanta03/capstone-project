pipeline {
    agent any

    stages {

        stage('Job1 - Build') {
            steps {
                echo 'Building Docker image'

                sh 'docker build -t mywebapp .'
            }
        }

        stage('Job2 - Test') {
            steps {
                echo 'Testing application'

                sh '''
                    docker rm -f mywebapp || true

                    docker run -d --name mywebapp -p 8081:80 mywebapp

                    sleep 5

                    curl -f http://localhost:8081

                    docker rm -f mywebapp
                '''
            }
        }

        stage('Job3 - Deploying to Prod') {
            when {
                branch 'main'
            }

            steps {
                echo 'Deploying to production'

                sh '''
                    docker rm -f webapp || true

                    docker run -d  --name webapp -p 8081:80 mywebapp
                     
                '''
            }
        }
          
    }
}
