pipeline{

    agent {label 'linux'}

    environment {
        DOCKERHUB_CREDENTIALS=credentials('docker')
    }

    stages {

        stage('gitclone')  {

            steps {
                git 'https://github.com/southyaga/pushdockerproject.git'
            }
        }

        stage('Build') {

            steps {
                sh 'docker build -t southyaga/stws_apache:latest .'
            }
        }

        stage('Login') {
            
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USE --password-stdin'
            }
        }

        stage('Push') {

            steps {
                sh 'docker push southyaga/stws_apache:latest'
            }
        }
    }

    post{
        always {
            sh 'docker logout'
        }
    }

}
