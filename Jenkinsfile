pipeline {
    agent any // just says we can run on any agent

    triggers { pollSCM('* * * * *') }

    stages {
        // checkout stage not needed as file is within the repo, checkout will occur automatically
        /*stage('Checkout') {
             steps {
                 git branch: 'main', url: 'https://github.com/hannahliz/jgsu-spring-petclinic.git'
             }
         }*/

        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
        post {
            // 'success' for on success or 'failure' for on failure
            // 'fixed' (previous failed, current succeeded)
            // 'regression' (current worse than last)
            // 'changed' (combines both 'fixed' and 'regression')
            always {
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts 'target/*.jar'
            }
        }
    }
}
