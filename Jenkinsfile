pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mvn383"
    }

    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/spring-projects/spring-petclinic.git'

                sh "mvn verify"
                // To run Maven on a Windows agent, use
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
                sh "echo $JFROG_HOME"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        } 
    }
}
