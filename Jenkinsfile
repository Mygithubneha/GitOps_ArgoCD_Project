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
                    script{
                        docker_image = docker.build "${IMAGE_NAME}"
                    }
                    
                }
            }

            stage('Push docker image') {
                steps {
                    script{
                        docker.withRegistry('',REGISTRY_CRED){
                        docker_image.push("$BUILD_NUMBER")
                        docker_image.push('latest')
                    }
                    
                    }
                }
            }

            stage('Delete Docker images'){
                steps{
                    script{
                        sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"
                        sh "docker rmi ${IMAGE_NAME}:latest"
                    }
                }
            
            }

            stage('Updating Kubernetes deployment file'){
                steps{
                    script{

                        sh """
                        cat deployment.yml
                        sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yml
                        cat deployment.yml
                        """
                    }
                }
            }

            stage('Push the changed deployment file to Git'){
                steps{
                    script{
                        sh """
                        git config --global user.name "neha"
                        git config --global user.email "neha@gmail.com"
                        git add deployment.yml
                        git commit -m "Updated the deployment file"
                        """
                        withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                            sh "git push https://github.com/Mygithubneha/GitOps_ArgoCD_Project.git main"
                        }
                    }
                }
            }
    }
}


//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