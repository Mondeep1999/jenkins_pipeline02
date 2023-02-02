pipeline {
    agent any

    stages{
        stage('Build-image'){
            steps{
                script{
                    sh 'docker build -t alphax123/docker-image-autobuild:jenkins-pipeline .'
                }
            }
        }
        stage('Push-to-Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u javatechie -p ${dockerhubpwd}'

}
                   sh 'docker push alphax123/docker-image-autobuild:jenkins-pipeline'
                }
            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
                }
            }
        }
    }
}
