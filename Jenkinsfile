pipeline {
agent any
tools {
maven 'Maven'
}
stages {
stage('Initialize'){
steps {
sh '''
      echo "PATH =${PATH}"
      echo "M2_HOME =${M2_HOME}"
'''
}
}
      stage('Build'){
      steps{
sh 'mvn clean package'
}
}
      stage('Deploy-to-tomcat')
      {
            Steps{
             sshagent(['tomcat'])
                  {
                   sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.233.108.223:/home/ubuntu/apache-tomcat-8.5.63/webapps'    
                  }
            }
      }
}
}
