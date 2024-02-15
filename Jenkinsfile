pipeline {
            agent {
                node {
                    label 'nodiono'
                }
            }
            stages {
                stage('Conenctar nodo docker') {
                    steps {
                        sh 'echo "hola"';
                        sh 'scp /opt/jenkins/workspace/nodonio lautaro@172.17.0.4:/home/lautaro/';
                    }
                }
            }
        }
