pipeline {
    agent { label 'master' }
    stages {
        stage('build') {
            steps {
              sh '''#!/bin/bash
                    cd ../source-repo
                    MSG=$(git log -1 --format=%B)
                    cd ..
                    rsync -avr --exclude='.git' --exclude='.github' --delete source-repo/. target-repo
                    cd target-repo
                    git checkout release-candidate
                    git config user.email "robot@powerdms.net"
                    git config user.name "Looker Content Sync Robot"
                    git add .
                    git commit -m "${MSG}"
                    git push"
                   '''
            }
        }
    }
