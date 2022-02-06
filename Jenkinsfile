#!/usr/bin/env groovy
// shebang tells most editors to treat as groovy (syntax highlights, formatting, etc)

pipeline {
    agent any
    triggers { pollSCM('* * * * *') }
    stages {
        // implicit checkout stage

        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
    }
    // post after stages, for entire pipeline, is also an implicit step albeit with explicit config here, unlike implicit checkout stage
    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
        }
//        changed {
//            emailext subject: "Job \'${JOB_NAME}\' (${BUILD_NUMBER}) ${currentBuild.result}",
//                    body: 'Please go to ${BUILD_URL} and verify the build',
//                    attachLog: true,
//                    compressLog: true,
//                    to: 'devops@acme.com',
//                    recipientProviders: [upstreamDevelopers(), requestor()]
//        }
    }
}
