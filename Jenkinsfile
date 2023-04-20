pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'pretei45', url: 'https://github.com/pretei45/mavenjob.git']])
      }
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
  -Dsonar.host.url=http://ec2-3-12-111-129.us-east-2.compute.amazonaws.com:9000 \
  -Dsonar.token=sqp_5f050fa78f0cbfe9516e2c147a767e4a882d5a98"
      }
    }
  }
}
