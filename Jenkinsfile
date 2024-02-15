pipeline {
            agent {
                node {
                    label 'nodiono'
                }
            }
            stages {
                stage('Conenctar nodo docker') {
                    steps {
                        env.SSH_PASSWD = 'contraseña_lautaro'
                        sh 'echo "hola"';
                        sh 'sshpass -p $SSH_PASSWD scp /opt/jenkins/workspace/nodonio lautaro@172.17.0.4:/home/lautaro/';
                    }
                }
            }
        }
