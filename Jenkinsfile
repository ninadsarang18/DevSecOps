pipeline {
agent any
tools {
maven 'Maven'
}
stages {
stage('Initialize')
      {
steps {
sh '''
      echo "PATH =${PATH}"
      echo "M2_HOME =${M2_HOME}"
'''
}
}
stage('Check-Secrets')
      {
            steps {
                  sh 'rm Secrets || true'
                  sh 'docker run dxa4481/trufflehog --json https://github.com/ninadsarang18/DevSecOps.git > Secrets'
                  sh 'cat Secrets'
            } 
      }
stage('SOURCE_Composition_Analysis')
      {
      steps 
            {
            sh 'rm owasp* || true'
            sh 'wget 'https://raw.githubusercontent.com/ninadsarang18/DevSecOps/master/OwaspDC_SCA''
            sh 'chmod +x OwaspDC_SCA.sh'
            sh 'bash OwaspDC_SCA.sh'
            }
      }
      stage('Build')
      {
            steps{
                  sh 'mvn clean package'
                  }
      }
stage('Deploy-to-tomcat')
      {
            steps
            {
             sshagent(['TOMCAT'])
                  {
                   sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.232.33.20:/home/ubuntu/apache-tomcat-8.5.63/webapps/webapps.war'    
                  }
            }
      }
}
}
