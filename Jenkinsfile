

String verRegex = /^DCV-(\d{1}[.]\d{1}|\d{1}[.]\d{1}[.]\d{1})/
String verRC = /^([0-9]+).([0-9]+).([0-9]+)-(rc[0-9]+)/
String verGA = /^([0-9]+).([0-9]+).([0-9]+)/

println("branch: ${env.BRANCH_NAME}")

def param1 = "param1"
def param2 = "param2"

if ("${env.BRANCH_NAME}" =~ verRC) {
    println("rc version")
    param1 = "RC1"
    param2 = "RC2"
} else if ("${env.BRANCH_NAME}" =~ verGA) {
    println("GA version")
    param1 = "GA1"
    param2 = "GA1"
}

pipeline {
    agent {
        label 'general'
    }

    parameters {
        string(name: 'param1', defaultValue: "$param1", description: 'Number of minutes pod will stay idle post build'),
        string(name: 'param2', defaultValue: "$param2", description: 'Number of minutes pod will stay idle post build')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'

                sh """#!/bin/bash -l

                COMMIT_LONG=`git log -n 1 HEAD --pretty=format:\"%H\"`
                COMMIT_SHORT=\${COMMIT_LONG:0:7}
                CURRENT_BRANCH=`git reflog show --all | grep \$COMMIT_SHORT | awk -F '@' {'print \$1'} | awk -F '/' {'print \$NF'}`
                echo "Current Branch: \$CURRENT_BRANCH"
                
                """
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
