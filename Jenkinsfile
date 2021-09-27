#!/usr/bin/env groovy
pipeline {
    
    
    stages {
        stage("Prepare") {
            steps {
                sh "echo test"
            }
        }
    }

    post {
        always {
            sh "docker-compose down || true"
        }

        success {
            bitbucketStatusNotify buildState: "SUCCESSFUL"
        }

        failure {
            bitbucketStatusNotify buildState: "FAILED"
        }
    }
}