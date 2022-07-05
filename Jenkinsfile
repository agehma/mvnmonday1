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
    }
}

