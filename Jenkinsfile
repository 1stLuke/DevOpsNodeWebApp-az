pipeline {
    agent any

    stages {
        stage('Docker Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-1stluke', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            export DOCKER_HOST=tcp://host.docker.internal:2375
                            docker login -u $USERNAME -p $PASSWORD
                            docker push 1stluke/node-web-app-2
                        '''
                    }
                }
            }
        }
        stage('Trigger Render Deployment') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'RenderDeployKey', variable: 'KEY')]) {
                        sh "curl https://api.render.com/deploy/$KEY"
                    }
                }
            }
        }        
    }
}
