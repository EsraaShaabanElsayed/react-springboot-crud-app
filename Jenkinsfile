pipeline {
    agent any
    environment {
        VM_IP = '172.16.62.133'
        SSH_CREDENTIALS = 'jenkins-key'
        BACKEND_DIR = '/opt/app/backend/'
        FRONTEND_DIR = '/var/www/html/'
    }
    tools {
        nodejs "node"
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/EsraaShaabanElsayed/react-springboot-crud-app.git'
            }
        }
        stage('Build Spring Boot') {
            steps {
                dir('crud-example-backend') {
                    sh './mvnw clean package'
                }
            }
        }
        stage('Build React App') {
            steps {
                dir('crud-example-frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        stage('Deploy Spring Boot') {
            steps {
                script {
                    sshagent([ 'jenkins-key']) {
                        // Copy the JAR file to the remote server
                        sh "scp crud-example-backend/target/*.jar ${SSH_USER}@${VM_IP}:${BACKEND_DIR}"

                        // Stop the currently running Spring Boot application (if any) and start the new one
                        sh """
                        ssh ${SSH_USER}@${VM_IP} '
                            pkill -f "java -jar ${BACKEND_DIR}*.jar" || true
                            java -jar ${BACKEND_DIR}*.jar > /dev/null 2>&1 &
                        '
                        """
                    }
                }
            }
        }
        stage('Deploy React App') {
            steps {
                script {
                    sshagent([ 'jenkins-key']) {
                        // Copy React build files to the server
                        sh "scp -r crud-example-frontend/build/* ${SSH_USER}@${VM_IP}:${FRONTEND_DIR}"

                        // Restart Nginx to serve the new build
                        sh "ssh ${SSH_USER}@${VM_IP} 'sudo systemctl restart nginx'"
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
