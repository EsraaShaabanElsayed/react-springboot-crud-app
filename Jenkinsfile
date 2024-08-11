pipeline {
    agent any
    environment {
        VM_IP = '172.16.62.133'
        SSH_CREDENTIALS = 'jenkins-key'
        SSH_USER = 'esraa'
        BACKEND_DIR = '/opt/app/'
        FRONTEND_DIR = '/var/www/html/'
        VERSION = '0.0.1-SNAPSHOT'  // Define the version here
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
                    sh 'chmod +x mvnw'
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
                    sshagent([SSH_CREDENTIALS]) {
                        // Copy the JAR file to the remote server
                        sh "scp crud-example-backend/target/crud-example-${VERSION}.jar ${SSH_USER}@${VM_IP}:${BACKEND_DIR}"

                        // Ensure the JAR file is executable and start it
                        sh """
                        ssh ${SSH_USER}@${VM_IP} '
                            # Make sure the JAR file is executable
                            chmod +x ${BACKEND_DIR}crud-example-${VERSION}.jar
                            
                            # Start the new application
                            nohup java -jar ${BACKEND_DIR}crud-example-${VERSION}.jar > ${BACKEND_DIR}app.log 2>&1 &
                        '
                        """
                    }
                }
            }
        }
        stage('Deploy React App') {
            steps {
                script {
                    sshagent([SSH_CREDENTIALS]) {
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
