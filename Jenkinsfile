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
                                   sshagent(['tomcat-new]){ // in jenkins goto --> snippet Generator ---> in sample step select ssh agent--->credentials---> select ssh username with private key-->id name: tomcat-new--> username (ec2-user) --->key(paste pem.key of tomcat server)--->generate pipeline script.
                                   sh """
                                   scp -o StrictHostKeyChecking-no target/myweb.war ec2-user@172.31.38.118:/home/ec2-user/apache-tomcat-9.0.46/webapps/ [//tomcat instance private ip]
                                   ssh ec2-user@172.31.38.118:/home/ec2-user/apache-tomcat-9.0.46/shutdown.sh
                                   ssh ec2-user@172.31.38.118:/home/ec2-user/apache-tomcat-9.0.46/startup.sh
                                   """
                                   }
                                }
                            }
}
