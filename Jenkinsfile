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

    
    stage ('software composition analysis'){
        steps{
            sh 'wget https://raw.githubusercontent.com/Nikz018/webapp/master/owasp-dependency-check.sh'
            sh 'chmod +x owasp-dependency-check.sh'
            sh 'bash owasp-dependency-check.sh'
            sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        }
    }
        stage('Build') {
            steps{
           sh 'mvn clean package'
            }
        }

    }
}
