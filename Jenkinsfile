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
                stage('Push to GitHub') {
            steps {
                script {
                    // Clonar el repositorio desde GitHub
                    sh 'git config --global user.email "lalor07@gmail.com"'
                    sh 'git config --global user.name "Tu Nombre"'
                    git 'https://tu-usuario:tu-token@github.com/tu-usuario/tu-repositorio.git'

                    // Hacer las modificaciones necesarias en el archivo
                    sh 'echo "Contenido modificado" > miarchivo.txt'

                    // Hacer commit y push de los cambios
                    sh 'git add miarchivo.txt'
                    sh 'git commit -m "Actualizar archivo desde Jenkins"'
                    sh 'git push origin nombre-de-tu-rama'
                }
            }
        }
    }
    
}
