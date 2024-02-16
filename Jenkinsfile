pipeline {
    agent {
        node {
            label 'nodiono'
        }
    }
    environment {
        SSH_PASSWD = '12345'
        GIT_CREDENTIALS = credentials('tokengit')
        GIT_USERNAME = 'Lauty04'
        GIT_PASSWORD = 'Lauti2004#'
        
        
    }
    stages {
        stage('Connect to Docker Node') {
            steps {
                script {
                    sh 'pwd';
                    sh 'chmod +x /opt/jenkins/workspace/nodonio/python-diff.py';
                    sh './python-diff.py old.xlsx new.xlsx'
                    echo "Python script completed..."
                    sh 'bash ';
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
                            withCredentials([usernamePassword(credentialsId: 'tokengit', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                                sh 'git config --global user.email "lalor07@gmail.com"'
                                sh 'git config --global user.name "Lauty04"'
                                sh 'git add logs.pdf'
                                sh 'git commit -m "Actualizar archivo desde Jenkins"'
        
                                // Delete existing tag if it exists
                                //sh 'git tag -d somun  || true'
        
                                sh 'git tag -a somu -m "Jenkins"'
                                
                                // Check if 'main' branch exists, create it if not
                                sh 'git rev-parse --verify main || git branch main'
                                
                                // Checkout 'main' branch and pull changes
                                sh 'git checkout main'
                                sh 'git pull https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Lauty04/exels.git main'
                                
                                // Push changes to 'main' branch
                                sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Lauty04/exels.git --tags'
                                sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/Lauty04/exels.git main'
                            }
                }
    }
}




    }
    
}
