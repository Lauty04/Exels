pipeline {
            agent {
                node {
                    label 'nodiono'
                }
            }
            stages {
                stage('Conenctar nodo docker') {
                    steps {
                        sh 'env.SSH_PASSWD = '12345'';
                        sh 'echo "hola"';
                        sh 'sshpass -p $SSH_PASSWD scp /opt/jenkins/workspace/nodonio lautaro@172.17.0.4:/home/lautaro/';
                    }
                }
            }
        }
