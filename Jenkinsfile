pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                dir('/mnt/workspace/2025Q2') {
                    echo "Cleaning workspace..."
                    sh 'rm -rf /mnt/workspace/2025Q2/*'

                    echo "Cloning repository..."
                    git(
                        branch: '2025Q2',
                        credentialsId: 'c0863cd8-559e-4921-a41f-62943a59d72a',
                        url: 'https://github.com/KunalGKNY/Docker-Multibranch.git'
                    )
                }
            }
        }
    }
}
