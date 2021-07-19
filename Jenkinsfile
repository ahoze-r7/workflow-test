pipeline {
    agent {
        label 'general'
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
