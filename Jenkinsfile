pipeline
{
    agent any
    stages
    {
        stage('ContDown')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDep')
        {
            steps
            {
                sh 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline1/webapp/target/webapp.war ubuntu@172.31.2.109:/var/lib/tomcat9/webapps/mytestapp.war'
            }
        }
        stage('ContTest')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContDely')
        {
            steps
            {
                input message: 'Need approvals from the DM!', submitter: 'srinivas'
                sh 'scp /home/ubuntu/.jenkins/workspace/DeclarativePipeline1/webapp/target/webapp.war ubuntu@prodprivateip:/var/lib/tomcat9/webapps/myprodapp.war'
            }
        }
    }
}
