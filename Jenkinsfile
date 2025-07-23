pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git credentialsId: '3ed9844a-5ef1-4a41-b039-5db654cd6252', url: 'https://github.com/KunalGKNY/2025Q2.git'
            }
        }

        stage('Build and Deploy Container') {
            steps {
                script {
                    // Identify the branch and define container name and port
                    def branch = env.BRANCH_NAME
                    def containerName = ""
                    def hostPort = ""

                    if (branch == "2025Q1") {
                        containerName = "c1"
                        hostPort = "80"
                    } else if (branch == "2025Q2") {
                        containerName = "c2"
                        hostPort = "90"
                    } else if (branch == "2025Q3") {
                        containerName = "c3"
                        hostPort = "8080"
                    } else {
                        error("Branch ${branch} not handled.")
                    }

                    // Remove existing container if it exists (idempotent)
                    sh "docker rm -f ${containerName} || true"

                    // Run new container with updated index.html
                    sh '''
                        mkdir -p /tmp/webcontent
                        cp index.html /tmp/webcontent/
                        docker run -d \
                            --name ${containerName} \
                            -p ${hostPort}:80 \
                            -v /tmp/webcontent:/usr/local/apache2/htdocs/ \
                            httpd
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "Deployment completed successfully."
        }
        failure {
            echo "Deployment failed. Please check the logs."
        }
        always {
            echo "Pipeline execution finished."
        }
    }
}
