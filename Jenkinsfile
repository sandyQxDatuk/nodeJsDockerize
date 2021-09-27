#!/usr/bin/env groovy
pipeline {
    agent { node { label 'swarm-ci' } }

    environment {
        TEST_PREFIX = "test-IMAGE"
        TEST_IMAGE = "${env.TEST_PREFIX}:${env.BUILD_NUMBER}"
        TEST_CONTAINER = "${env.TEST_PREFIX}-${env.BUILD_NUMBER}"
        REGISTRY_ADDRESS = "my.registry.address.com"

        SLACK_CHANNEL = "#deployment-notifications"
        SLACK_TEAM_DOMAIN = "MY-SLACK-TEAM"
        SLACK_TOKEN = credentials("slack_token")
        DEPLOY_URL = "https://deployment.example.com/"

        COMPOSE_FILE = "docker-compose.yml"
        REGISTRY_AUTH = credentials("docker-registry")
        STACK_PREFIX = "my-project-stack-name"
    }

    stages {
        stage("Prepare") {
            steps {
                echo "test"
            }
        }

        stage("Build and start test image") {
            steps {
                echo "test"
            }
        }

        stage("Run tests") {
            steps {
                echo "test"
            }

            
        }

        stage("Determine new version") {
            when {
                branch "master"
            }

            steps {
                script {
                    echo "test"
                }
            }
        }

        stage("Create new version") {
            when {
                branch "master"
                echo "test"
            }

            steps {
                script {
                    echo "test"
                }

                
            }
        }

        stage("Deploy to production") {
            
            when {
                branch "master"
                echo "test"
            }

            steps {
                echo "test"
            }

            post {
                success {
                    slackSend(
                            teamDomain: "${env.SLACK_TEAM_DOMAIN}",
                            token: "${env.SLACK_TOKEN}",
                            channel: "${env.SLACK_CHANNEL}",
                            color: "good",
                            message: "${env.STACK_PREFIX} production deploy: *${env.DEPLOY_VERSION}*. <${env.DEPLOY_URL}|Access service> - <${env.BUILD_URL}|Check build>"
                    )
                }

                failure {
                    slackSend(
                            teamDomain: "${env.SLACK_TEAM_DOMAIN}",
                            token: "${env.SLACK_TOKEN}",
                            channel: "${env.SLACK_CHANNEL}",
                            color: "danger",
                            message: "${env.STACK_PREFIX} production deploy failed: *${env.DEPLOY_VERSION}*. <${env.BUILD_URL}|Check build>"
                    )
                }
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