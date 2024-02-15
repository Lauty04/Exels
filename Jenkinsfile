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
                    sh 'chmod +x /opt/jenkins/workspace/nodonio/python-diff.py';
                    sh './opt/jenkins/workspace/nodonio/python-diff.py /opt/jenkins/workspace/nodonio/old.xlsx /opt/jenkins/workspace/nodonio/new.xlsx'
                    echo "Python script completed..."
                    sh 'bash ';
                    sh "sshpass -p $SSH_PASSWD scp -o StrictHostKeyChecking=no /opt/jenkins/workspace/nodonio/meta-script.sh lautaro@172.17.0.4:/home/lautaro/"
                    // sh 'ssh lautaro@172.17.0.4 "bash meta-script.sh "';
                }
            }
        }
    }
}
