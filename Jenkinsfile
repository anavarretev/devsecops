pipeline {
    agent any

    tools {
        maven 'Maven'
        nodejs "NodeJs"
    }
  stages {
   stage ('Initial') {
            steps {
              sh '''
                   echo "PATH = ${PATH}"
                   echo "M2_HOME = ${M2_HOME}"
               '''
            }
        }
        stage ('Compile') {
            steps {
                 sh 'mvn clean compile -e'
            }
        }
      stage('Test'){
            steps{
                figlet 'Test'
                sh 'mvn clean test -e'
            }
        }
      stage('SCA'){
            steps{
                figlet 'Dependency-Check'
                sh 'mvn org.owasp:dependency-check-maven:check'
                
                archiveArtifacts artifacts: 'target/dependency-check-report.html', followSymlinks: false
            }
        }
    }
}
