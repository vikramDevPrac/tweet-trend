pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/maven/bin:$PATH" 
}
    
    stages  {
        stage('Build') {
            steps {
                sh 'mvn clean deploy'
            }
        }

        stage('SCM') {
            git 'https://github.com/foo/bar.git'
        }
        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'vikramdevops-sonar-scanner'
            }
            steps{
            withSonarQubeEnv('vikramdevops-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
                sh "${scannerHome}/bin/sonar-scanner"
            }
            }
        }

    }

}