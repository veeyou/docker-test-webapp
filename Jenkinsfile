pipeline{
  agent any
  stages{
    stage('checkout'){
      steps{
        checkout scm
      }
    }
    stage('build'){
      steps{
        sh "./gradlew clean build"
      }
    }
    stage('build&&push image'){
      steps{
        echo "build image"
        sh "docker build -t test-webapp:${env.BUILD_ID}."
      }
    }
    stage('deploy'){
      steps{
        sh "docker stop test-webapp||true"
        sh "docker rm test-webapp||true"
        sh "docker run -d --name test-webapp -p 8001:8080 test-webapp:${env.BUILD_ID}"
      }
    }
  }
}
          
