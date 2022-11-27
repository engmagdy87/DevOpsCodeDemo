pipeline {
  tools {
    maven 'mymaven'
  }
  agent any
  stages {
    stage('Clone the repo') {
      steps {
        echo 'cloning'
        git 'https://github.com/Sonal0409/DevOpsClassCodes.git'
      }
    }
    stage('Compile') {
      steps {
        echo 'complie the code..'
        sh 'mvn compile'
      }
    }
    stage('UnitTest') {
      steps {
        sh 'mvn test'
      }
      post {
        success {
          junit 'target/surefire-reports/*.xml'
        }
      }
    }
    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }
    stage('Deploy') {
      steps {
        sshagent(['tomcatId']) {
          sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/2-ci-cd-pipeline-with-jenkins-simplilearn-assignment/target/addressbook.war ec2-user@18.216.225.163:/opt/tomcat/webapps'
        }
      }
    }
  }
}
