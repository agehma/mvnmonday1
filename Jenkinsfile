pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/agehma/mvnmonday1.git'
                    }
                    catch (Exception e1)
                    {
                        mail bcc: '', body: 'first download failed', cc: '', from: '', replyTo: '', subject: 'git failed', to: 'gt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch (Exception e2)
                    {
                        mail bcc: '', body: 'mvn failed to build artifact', cc: '', from: '', replyTo: '', subject: 'mvn failed', to: 'dvt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '3933de1f-781a-4384-bab7-5258db7fbfd3', path: '', url: 'http://172.31.85.178:8080')], contextPath: 'testapp', war: '**/*.war'
                    }
                    catch (Exception e3)
                    {
                        mail bcc: '', body: 'qa tomcat server failed to deploy', cc: '', from: '', replyTo: '', subject: 'qa tomcat failed', to: 'mwt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/agehma/testingscript1.git'
                        sh 'java -jar /var/lib/jenkins/workspace/DeclarativePE/testing.jar'
                    }
                    catch (Exception e4)
                    {
                        mail bcc: '', body: 'selenium failed to test', cc: '', from: '', replyTo: '', subject: 'selenium failed', to: 'st@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '3933de1f-781a-4384-bab7-5258db7fbfd3', path: '', url: 'http://172.31.85.56:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                    catch (Exception e5)
                    {
                        mail bcc: '', body: 'delivery failed into prodserver', cc: '', from: '', replyTo: '', subject: 'delivery failed', to: 'dt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
    }
}

