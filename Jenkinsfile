pipeline
{
    agent any
    stages
      {
          stage ('Cont-Download')
          {
              steps
              {
                  git 'https://github.com/IntelliqDevops/mymaven.git'
              }
          }
          stage ('Cont-Build')
          {
              steps
              {
                  sh 'mvn package'
              }
          }
          stage ('Cont-Deployment')
          {
              steps
              {
                  deploy adapters: [tomcat9(credentialsId: 'd84ed1ec-d7e1-4011-914b-efef0fd55f09', path: '', url: 'http://172.31.4.123:8080')], contextPath: 'testapp1', war: '**/*.war' 
              }
              
          }
          stage ('Cont-Testing')
          {
              steps
              {
                  git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                  
                  sh 'java -jar /var/lib/jenkins/workspace/Declarativepipeline/testing.jar'
                  
              }
          }
          stage ('Cont-Delivery')
          {
              steps
              {
                  deploy adapters: [tomcat9(credentialsId: 'd84ed1ec-d7e1-4011-914b-efef0fd55f09', path: '', url: 'http://172.31.11.230:8080')], contextPath: 'prodapp1', war: '**/*.war'
              }
          }
      }
}
