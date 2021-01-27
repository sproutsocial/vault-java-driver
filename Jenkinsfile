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

//         stage('Package & Publish') {
//             steps {
//                 script {
//
//                     withCredentials([usernamePassword(credentialsId: 'maven-username-password', passwordVariable: 'mvnPassword', usernameVariable: 'mvnUsername')]) {
//                         dockerRun = "docker run --rm -v \"${workspace}:/src\" -w /src $DOCKER_CONTAINER:$DOCKER_TAG"
//
//                         def gradleProperties = [
//                                 "org.gradle.jvmargs": "-Xmx1536m",
//                                 "android.useAndroidX": "true",
//                                 "android.enableJetifier": "true",
//                                 "kotlin.code.style": "official",
//                                 "SPROUT_NEXUS_USERNAME": mvnUsername,
//                                 "SPROUT_NEXUS_PASSWORD": mvnPassword
//                         ]
//
//                         // Drop in some config properties
//                         sh "echo 'sdk.dir=/usr/local/android-sdk' > local.properties"
//
//                         // Delete existing file, so we can append from a fresh state.
//                         sh "echo > gradle.properties"
//
//                         gradleProperties.each { k, v ->
//                             sh "echo \"${k}=${v}\" >> gradle.properties"
//                         }
//
//                         sh "${dockerRun} /bin/bash -c \"./gradlew :components:assembleRelease && ./gradlew publishMavenPublicationToSproutNexusRepository\""
//                     }
//                 }
//             }
//         }
    }
//
//     post {
//         success {
//             slackSend channel:slackChannel, color: 'good', message: "Success: ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
//         }
//         failure {
//             slackSend channel:slackChannel, color: 'bad', message: "Failure: ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
//         }
//     }
}