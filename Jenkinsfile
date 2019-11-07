pipeline {
   environment {
     registry = '<concealed>'
     registryCredential = '<concealed>'
     dockerImage = ''
   }
   agent any
   stages {
     stage('Cloning Git') {
       steps {
         checkout scm
       }
     }
     stage('Build image') {
       steps{
         script {
           dockerImage = docker.build registry + ":$BUILD_NUMBER"
         }
       }
     }
     stage('Push Image') {
       steps{
         script {
           docker.withRegistry( registry, registryCredential ) {
             dockerImage.push()
           }
         }
       }
     }
     stage('Remove Unused docker image') {
       steps{
         sh "docker rmi $registry:$BUILD_NUMBER"
       }
     }
   }
 }