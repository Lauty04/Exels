pipeline {
    agent {
        node {
            label 'nodiono'
        }
    }
    environment {
        SSH_PASSWD = '12345'
        GIT_CREDENTIALS = credentials('tokengit')
    }
    stages {
        stage('Connect to Docker Node') {
            steps {
                script {
                    sh 'pwd'
                    sh 'chmod +x /opt/jenkins/workspace/nodonio/python-diff.py'
                    sh './python-diff.py old.xlsx new.xlsx'
                    echo "Python script completed..."
                    sh 'bash '
                    sh "sshpass -p $SSH_PASSWD scp -o StrictHostKeyChecking=no /opt/jenkins/workspace/nodonio/meta-script.sh lautaro@172.17.0.4:/home/lautaro/"
                    // sh "sshpass -p $SSH_PASSWD ssh lautaro@172.17.0.4 'sudo su'" 
                    sh 'sshpass -p $SSH_PASSWD ssh lautaro@172.17.0.4 "chmod +x /home/lautaro/meta-script.sh "'
                    sh 'whoami'
                    sh "sshpass -p $SSH_PASSWD ssh lautaro@172.17.0.4 'bash /home/lautaro/meta-script.sh'"
                }
            }
        }
        stage('Convert MD to PDF') {
            steps {
                script {
                    sh 'pandoc logs.md --pdf-engine=xelatex -o logs.pdf'
                }
            }
        }
        stage('Push to GitHub') {
            steps {
                script {
                    sh 'git config --global user.email \'lalor07@gmail.com\''
                    sh 'git config --global user.name \'Lauty04\''
                    sh 'git add logs.pdf'
                    sh 'git commit -m "Añadido"'
                    withCredentials([usernamePassword(credentialsId: 'tokengit', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Lauty04/exels.git HEAD:main')
                    }
                }
            }
        }
        stage('Telegram message') {
            steps {
                script {
                    def chatId = '5419757145'
                    def token = '6421695221:AAFvC_xdV-RTxlAuH0_Fdahu0TMLXFHkWgU'
                    message = 'We don´t know'
                    if (currentBuild.resultIsBetterOrEqualTo('SUCCESS')) {
                        message = 'The work is completed'
                    } else {
                        message = 'Failed work'
                    }
                    sh "curl -X POST -H 'Content-Type: application/json' -d '{\"chat_id\": \"${chatId}\", \"text\": \"${message}\", \"disable_notification\": false}' https://api.telegram.org/bot${token}/sendMessage";

                }
            }
        }
    }
}
