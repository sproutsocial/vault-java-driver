/*
 * Jenkinsfile are written in Groovy (http://www.groovy-lang.org/)
 * When wring the file you have access to all of the Groovy langauge
 * constructs as well as some extra Jenkins-provided variables and methods
 */

/*
 * The file must have at least one 'node' that tells Jenkins where to run
 * the subsequent commands. The string provided to the node() function
 * can be a specific jenkins node name (ie 'worker01') or one or more
 * Jenkins node labels. Here the job described below will run on any
 * Jenkins node with the `docker` label. Labels for nodes are managed from
 * within the Jenkins web-UI.
 */

def dockerRun

def slackChannel = "#eng-dbre"

pipeline {
    agent {
        node {
            label 'docker'
        }
    }

    stages {
        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }

        stage('Build/Push Docker Images') {
            steps {
                sh "docker run --rm -it -v ${workspace}:/src -w /src gradle:6.8.1-jdk11 gradle build"
            }
        }
    }
}