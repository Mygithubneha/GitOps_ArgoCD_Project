pipeline {

    agent any

    environment {

        DOCKERHUB_USERNAME = "mydockerhub121"
        APP_NAME = "gitops-argo-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CRED = 'dockerhub'
    }
        stages {

            stage('CleanWorkspace') {
                steps {
                    cleanWs()
            }
        }

            stage('Code checkout from SCM') {
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/Mygithubneha/GitOps_ArgoCD_Project.git'
                }
            }

            stage('Build docker image') {
                steps {
                    docker_image = docker.build "${IMAGE_NAME}"
                }
            }

            stage('Push docker image') {
                steps {
                    docker.withRegistry('',REGISTRY_CRED){
                        docker_image.push("$BUILD_NUMBER")
                        docker_image.push('latest')
                    }
                }
            }
    }
}


//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