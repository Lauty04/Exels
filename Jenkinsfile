pipeline {
    agent {
        node {
            label 'nodiono'
        }
    }
    environment {
        SSH_PASSWD = '12345'
    }
    stages {
        stage('Connect to Docker Node') {
            steps {
                script {
                    echo "Hello"
                    sh 'bash ';
                    sh "sshpass -p $SSH_PASSWD scp -o StrictHostKeyChecking=no /opt/jenkins/workspace/nodonio/* lautaro@172.17.0.4:/home/lautaro/"
                    sh 'ssh lautaro@172.17.0.4 "bash python-diff.py old.xlsx new.xlsx "';
                }
            }
        }
    }
}
