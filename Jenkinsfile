pipeline {

  agent any
  environment {
      PATH = "/opt/maven/bin:$PATH"
  }
  stages {
      stage("git"){
          steps{
            git branch: 'main', url: 'https://github.com/vamsibyramla/sample.git'
          
          }
      }
      stage("build"){
          steps{
              sh "mvn clean package"
          }
      }
      stage("deploy"){
          steps{
              deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://3.14.146.100:8081/')], contextPath: 'test', war: '**/*.war'
          }
      }
  }
}