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
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/Nikz018/webapp.git > trufflehog'
        sh 'cat trufflehog'
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
