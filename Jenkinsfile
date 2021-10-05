pipeline {
    environment{
    registry = "gospelmike/myapp"
    registryCredential = 'dockerhub'
    dockerImage = ''
    }
    agent any
    tools { 
        maven 'M2_HOME'
    }
    stages{
        stage('Git Checkout'){
            steps{
                git 'https://github.com/gospelmike/Kubernetes'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn -f MyAwesomeApp/pom.xml clean install'
            }
        }
        stage('Building image'){
          steps{
             script {
               dockerImage = docker.build registry + ":$BUILD_NUMBER" , "MyAwesomeApp"
             }
          }
        }
        stage('Push Image'){
          steps{
           script {
              docker.withRegistry( '', registryCredential ) {
                dockerImage.push("latest")
              }
            }
           }
        }
        stage('Remove Unused docker image') {
          steps{
            sh "docker rmi $registry:$BUILD_NUMBER"
          }
        }
        stage('Deploy in K8s'){
          steps{
            kubernetesDeploy(
                configs: 'MyAwesomeApp/Deployment.yml',
                kubeconfigId: 'K8S',
                enableConfigSubstitution: true
            )
          }
        }
    }
}
