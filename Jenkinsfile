pipeline{
    agent any
    stages {
        stage ("git checkout"){
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/Cloud-Lucky/nodejs-docker-app.git'
            }
        }
        stage ("docker build"){
            steps {
                sh 'docker build -t nodejs-jenkins-app .'
            }
        }
        stage ("docker push"){
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dokcer_Cred', passwordVariable: 'DockerPassword', usernameVariable: 'Dockerhub')]) {
               sh '''
               echo $DockerPassword | docker login -u $Dockerhub --password-stdin
               docker tag nodejs-jenkins-app $Dockerhub/nodejs-jenkins-app:latest
               docker push $dockerhub/nodejs-jenkins-app:latest
               '''
}
            }
        }
    }
}        
