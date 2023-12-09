pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Initialize') {
            steps {
                sh '''
                      echo "PATH = ${PATH}"
                      echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
       stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog1 || true'
        sh 'docker run zricethezav/gitleaks --json https://github.com/Nikz018/webapp.git > trufflehog1'
        sh 'cat trufflehog1'
      }
    }
    stage ('container-security') {
      steps {
        sh 'rm output.txt || true'
        sh 'docker run aquasec/trivy image zricethezav/gitleaks > output.txt'
        sh 'cat output.txt'
      }
    }
        stage('Build') {
            steps{
           sh 'mvn clean package'
            }
        }

    }
}
