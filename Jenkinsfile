pipeline {
    agent any

   tools {
      // Install the Maven version configured as "M3" and add it to the path
      maven "Maven"
   }
    stages {
        stage('Build') {
            steps {
            // Get some code from a GitHub repository
            git 'https://github.com/urmila1262/jenkins-git-integration/'

            // Run Maven on a Unix agent.
            sh "mvn -Dmaven.test.failure.ignore=true clean package"

            // To run Maven on a Windows agent, use
            // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy artifact into nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'jenkins-git-integration', classifier: '', file: '/Users/venugopal/.jenkins/workspace/mvn_test1/target/jenkins-git-integration.war', type: 'war']], credentialsId: 'ab0a9f6a-0f2e-45d8-a3a5-69b9937ae322', groupId: 'jenkins-git-integration', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-nexus-repo', version: '3.8.2'
            }
        }
    }
}
