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
                echo "-----------Build started-----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "-----------Build completed-----------"
            }
        }

        stage('test') {
            steps {
                echo "-----------Unit test started-----------"
                sh 'mvn surefire-report:report'
                echo "-----------Unit test compleed-----------"
            }
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