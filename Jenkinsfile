
pipeline {
    agent any
    stages {
        stage("checkout") {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'jenkins_github', url: 'https://github.com/priyanshi1006/dockerpipeline']])
            }
        }
        stage("Build Image") {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker build -t priyanshisavalia1006/dockerpipeline .'
                    } else {
                        bat 'docker build -t priyanshisavalia1006/dockerpipeline .'
                    }
                }
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'jenkins_pipeline', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    script {
                        if (isUnix()) {
                            sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                            sh 'docker push priyanshisavalia1006/dockerpipeline'
                            sh 'docker logout'
                        } else {
                            bat 'docker login -u %DOCKERHUB_USERNAME% -p %DOCKERHUB_PASSWORD%'
                            bat 'docker push priyanshisavalia1006/dockerpipeline'
                            bat 'docker logout'
                        }
                    }
                }
            }
        }
    }
}
