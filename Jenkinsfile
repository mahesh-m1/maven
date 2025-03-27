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
          stage ('Cont-Depoy')
          {
              steps
              {
                  deploy adapters: [tomcat9(credentialsId: 'ad72bc35-dfe8-4369-9091-7412c6ea4cb7', path: '', url: 'http://172.31.17.213:8080')], contextPath: 'testapp', war: '**/*.war'
              }
          }
          stage ('Cont-Test')
          {
              steps
              {
                  git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                  
                  sh 'java -jar /var/lib/jenkins/workspace/Declarativepipeline/testing.jar'
              }
          }
          stage ('Cont-Deploy')
          {
              steps
              {
                  deploy adapters: [tomcat9(credentialsId: 'ad72bc35-dfe8-4369-9091-7412c6ea4cb7', path: '', url: 'http://172.31.20.30:8080')], contextPath: 'prodapp', war: '**/*.war'
              }
          }
    }
}
