pipeline{
    agent any

        environment{
                    PATH = "/opt/maven3/bin:$PATH"
                    }
         sages{
                stage("Git Checkout"){
                steps{
                    git credentialsId: 'Hello', url: 'https://github.com/Naveen7702636896/Jenkinsdemo.git'
                      }
                }
          stage("Maven Build"){
                              steps{
                                    sh "mvn clean package"
                                    sh "mv target/*.war target/myweb.war"
                                    }
                                }
          stage("deploy dev"){
                             steps{
                                   sshagent(['Tomcat-server']){
                                   sh """
                                   scp -o StrictHostKeyChecking-no target/myweb.war ubuntu@172.31.47.97:/home/ubuntu/apache-tomcat-8.5.73/webapps/
                                   ssh ubuntu@172.31.47.97:/home/ubuntu/apache-tomcat-8.5.73/shutdown.sh
                                   ssh ubuntu@172.31.47.97:/home/ubuntu/apache-tomcat-8.5.73/startup.sh
                                   """
                                   }
                                }
                            }
}
