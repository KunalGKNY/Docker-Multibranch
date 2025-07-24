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
	
	
    stage('Docker setup') {
            steps {
               sh '''
			   
                   yum install -y docker || true
                   systemctl start docker || true
				   
                  '''
            }
    }
	
	
    stage('Docker container creations ') {
            steps {
               sh '''
			   
			     # Create container C2 if not exists
                 docker inspect C2 >/dev/null 2>&1 || docker run -dp 90:80 --name C2 httpd

				   
                  '''
            }
    }
	
	
	stage('Remove index.html from containers ') {
            steps {
               sh '''
			   
			     
                 docker exec C2 rm -rf /usr/local/apache2/htdocs/index.html || true
  
                  '''
            }
    }
	
	
	stage('coping the file in the container ') {
            steps {
               sh '''
			   
			     
                 docker cp /mnt/workspace/2025Q2/index.html C2:/usr/local/apache2/htdocs

                  '''
            }
    }

} 
		
} 
