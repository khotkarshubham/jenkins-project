pipeline {
    agent none

    stages {

        stage('Clone Code') {
            agent any
            steps {
                git 'https://github.com/khotkarshubham/jenkins-project.git'
            }
        }

        stage('Deploy on Both Agents') {
            parallel {

                stage('Agent1 Deploy') {
                    agent { label 'dockeragent' }
                    steps {
                        sh '''
                        echo "Deploying on Agent1"
                        hostname

                        docker rm -f container1 || true
                        docker build -t myimage .
                        docker run -d -p 8081:80 --name container1 myimage
                        '''
                    }
                }

                stage('Agent2 Deploy') {
                    agent { label 'agent2' }
                    steps {
                        sh '''
                        echo "Deploying on Agent2"
                        hostname

                        docker rm -f container2 || true
                        docker build -t myimage2 .
                        docker run -d -p 8082:80 --name container2 myimage2
                        '''
                    }
                }

            }
        }
    }
}
