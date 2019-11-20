pipeline
{
    agent {label "master"}
    options 
    {
        disableConcurrentBuilds()
    }
    stages
    {
        stage("Load ENV")
        {
            agent {label "master"}
            steps
            {
                script 
                {
					if (env.BRANCH_NAME == 'development') 
                    {
						load '/home/ubuntu/env/qa.groovy'
					} else if(env.BRANCH_NAME == 'master')
                    {
						load '/home/ubuntu/env/prod.groovy'
					}
                }
            }
        }
        stage("Install")
        {
            parallel
            {
                stage("FrontEnd")
                {
                    steps
                    {
                        echo "====++++FrontEnd====="
                    }
                }
                stage("FrontEnd-Server")
                {
                    steps
                    {
                        echo "====++++Frontend-Server++++===="
                    }
                }
                stage("Backend")
                {
                    steps
                    {
                        echo "====++++Backend++++===="
                    }
                }
                stage("ImapListener")
                {
                    steps
                    {
                        echo "====++++ImapListerner++++===="
                    }
                }
            }
        }
        stage("BuildOnSlave")
        {
            parallelBuild
            {
                stage("Build-Main")
                {
                   agent{label "aws"}
                   steps
                   {
                       echo "====++++Build-Main++++===="
                       sh 'ifconfig'
                    }
                }
                stage("Build-Agent")
                {
                    agent{label "aws"}
                    steps
                    {
                        echo "====++++Build-Agent++++===="
                        sh 'ifconfig'
                    } 
                }
                stage("Build-Manager")
                {
                    agent{label "aws"}
                    steps
                    {
                        echo "====++++Build-Manager++++===="
                        sh 'ifconfig'  
                    }
                }
                stage("Build-Admin")
                {
                    agent{label "aws"}
                    steps
                    {
                        echo "====++++Build-Admin++++===="
                        sh 'ifconfig'
                    }
                }
            }
        }
    }
}
