pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'staging',
                    url: 'git@github.com:akr-dco/deploytest-windows.git'
            }
        }

        stage('Prepare Target Folder') {
            steps {
                sshagent(credentials: ['ssh-jenkinsprod']) {
                    sh '''
                    ssh administrator@192.168.192.212 "cmd /c if not exist C:\\cicd\\test-deploy-windows mkdir C:\\cicd\\test-deploy-windows"
                    '''
                }
            }
        }

        stage('Deploy to Windows Server') {
            steps {
                sshagent(credentials: ['ssh-jenkinsprod']) {
                    sh '''
                    scp -r * administrator@192.168.192.212:/c/cicd/test-deploy-windows/
                    '''
                }
            }
        }
    }
}
