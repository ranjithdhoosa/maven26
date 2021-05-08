pipeline
{
    agent any
    stages
    {
        stage('CDownload_loans')
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
        stage('CBuild_loans')
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
        stage('CDeploy_loans')
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
                
    }
}
