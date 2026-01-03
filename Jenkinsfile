pipeline {
    agent any
    environment { 
        SERVER_IP = credentials('prod-server-ip')
    }

    stages {
            stage('Setup') {
            steps {
                sh "pip install --break-system-package -r requirements.txt"
            }
        }
        stage('test'){
            steps{
                sh "python3 -m pytest"
            }
        }
        stage('Package-code'){
            steps{
                sh "zip -r myapp.zip ./* -x '*.git*'"
                sh "ls -lart"
            }
        }
        stage('Deploy-to-prod'){
            steps{
                withCredentials([sshUserPrivateKey(credentialsId: 'ssh-key', keyFileVariable: 'MY_SSH_KEY',usernameVariable: 'username')]){
                sh '''
                sudo scp -i $MY_SSH_KEY -o StrictHostKeyChecking=no myapp.zip ${username}@${SERVER_IP}:/root
                sudo ssh -i $MY_SSH_KEY -o StrictHostKeyChecking=no ${username}@${SERVER_IP} <<
                EOF
                unzip -o /root/myapp.zip -d /root/GMS
                source GMS/venv/bin/activate
                cd /root/GMS
                pip install -r requirements.txt
                sudo systemctl restart flask.service
EOF
             '''
            }
            }
        }
    }
}

