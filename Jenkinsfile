pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'staging',
                    url: 'git@github.com:akr-dco/deploytest-windows.git'
            }
        }

        stage('Deploy to Windows Server') {
            steps {
                sshagent(credentials: ['ssh-jenkinsprod']) {
                    sh '''
                    rsync -av --delete ./ \
                    administrator@192.168.192.212:/c/cicd/test-deploy-windows/
                    '''
                }
            }
        }
    }
}
