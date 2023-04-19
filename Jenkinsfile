pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '60efebee-6fcc-4cfc-9ca1-6832fae996e6', url: 'https://github.com/olusolasp/MavenApp.git']])      }
    }
    stage('2-cleanws'){
      steps{
        sh 'mvn clean'
      }
    }
    stage('3-mavenbuild'){
      steps{
        sh 'mvn package'
      }
    }
      stage('unittest'){
        steps{
            sh 'mvn test'
        }
    }
    stage('sonarscanner'){
      steps{
      sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team5codereview \
  -Dsonar.projectName='team5codereview' \
  -Dsonar.host.url=http://ec2-54-67-23-205.us-west-1.compute.amazonaws.com:9000 \
  -Dsonar.token=sqp_50b194c0db00addbb98492848cb5ba3889ca2655"
      }
    }
  }
}
