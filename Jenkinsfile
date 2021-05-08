pipeline
{
    agent any
    stages
    {
        stage('CDownload')
        {
            steps
            {
                script
                {
                   try
                   {
                      git 'https://github.com/intelliqittrainings/maven.git'
                    }
                    catch(Exception e1)
                    {
                       mail bcc: '', body: 'jenkins job has failed', cc: '', from: '', replyTo: '', subject: '', to: 'ranjith.dhoosa@gmail.com'
                       exit(1)
                    }
                }    
            }
        }
        stage('CBuild')
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
                    mail bcc: '', body: 'jenkins job has failed', cc: '', from: '', replyTo: '', subject: '', to: 'ranjith.dhoosa@gmail.com'
                    exit(1)
                    }
                }
                
            }
        }
        stage('CDeploy')
        {
            steps
            {
                script
                {
                    try
                    {
                    deploy adapters: [tomcat9(credentialsId: 'f23b04ed-4dab-43ad-88ac-fece31432fee', path: '', url: 'http://172.31.82.201:8080')], contextPath: 'qaapp', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                    mail bcc: '', body: 'jenkins job has failed', cc: '', from: '', replyTo: '', subject: '', to: 'ranjith.dhoosa@gmail.com'
                    exit(1)
                    }
                }    
            }
        }
        stage('CTest')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/declarativepipeline2/testing.jar'
            }
        }
        stage('CDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'f23b04ed-4dab-43ad-88ac-fece31432fee', path: '', url: 'http://172.31.81.23:8080')], contextPath: 'prodaap', war: '**/*.war'
            }
        }
        
    }
}
