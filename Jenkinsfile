pipeline {
    agent { label 'master' }
    stages {
        stage('PROD') {
            environment {
                BUILD_REQUESTEDFOREMAIL = sh (script: 'git --no-pager show -s --format=\'%ae\'', returnStdout: true).trim()
                BUILD_REQUESTEDFOR = sh (script: 'git --no-pager show -s --format=\'%an\'', returnStdout: true).trim()
            }
            steps {
              sh '''#!/bin/bash
                    # set github user
                    git config user.email ${BUILD_REQUESTEDFOREMAIL}
                    git config user.name ${BUILD_REQUESTEDFOR}
                    git credentialsId: 'd017afeb-dcf8-4f4a-b73c-07d793e4628a', url: 'https://github.com/KuzRomanDocker/PROD
                    git remote -v
                    git remote add upstream https://github.com/KuzRomanDocker/PROD.git
                    git remote -v
                    git fetch upstream
                    git checkout master
                    git merge upstream/master
                    # push tag
                    git tag -a $BUILD_ID -m "Released by ${BUILD_REQUESTEDFOR}"
                    #git push origin $BUILD_ID
                   '''
            }
        }
    }
}
