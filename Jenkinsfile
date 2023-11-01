@Library(value='voyantic-jenkinsfile-utils', changelog=false) _

pipeline {
    agent { label 'Tagformance-TA' }
    triggers {
        githubPush()
        }
    environment {
        CERTIFICATE = credentials('voyantic-codesign-file-SHA1')
        PASS = credentials('voyantic-codesign-key')

    }
    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '10')
    }
    stages {
        stage('Checkout') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    retry(3) {
                        dir('voyantic-ci') {
                            checkout scm: [$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[credentialsId: 'jenkins-voyantic', url: 'git@github.com:voyantic/voyantic-ci.git']]], poll: false, changelog: false
                        }
                    }
                }
            }
        }
    }

}
