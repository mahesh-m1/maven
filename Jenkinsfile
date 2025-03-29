pipeline
{
    agent any
    stages
    {
        stage('Cont-Download')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/IntelliqDevops/maven1.git'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins was unable to download the repository from the git', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.admin@gmail.com'
                        exit(1)
                    }
                }
             }
        }
        stage('Cont-Build')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'Jenkins was unable to create a Artifact from the code', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'dev.admin@gmail.com'
                        exit(1)
                    }
                }
             }
        }
        stage('Cont-Deploy')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'scp /var/lib/jenkins/workspace/Declarativepipeline/webapp/target/webapp.war ubuntu@172.31.33.234:/var/lib/tomcat10/webapps/testapp.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins was unable to deploy into tomcat in testing servers', cc: '', from: '', replyTo: '', subject: 'Deploy Failed', to: 'middleware.admin@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('Cont-Testing')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                
                        sh 'java -jar /var/lib/jenkins/workspace/Declarativepipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Selinium scripts are failing ', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'qa.admin@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('Cont-Delivery')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'scp /var/lib/jenkins/workspace/Declarativepipeline/webapp/target/webapp.war ubuntu@172.31.37.219:/var/lib/tomcat10/webapps/prodapp.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins unable to deploy into tomcat on prod servers ', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'delivery.admin@gmail.com'
                    }
                }
             }
         }
     }
}
