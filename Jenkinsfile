pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                sh '''
                    echo "Hello World"
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                    # Update package lists
                    sudo apt-get update
                    
                    # Install Nginx
                    sudo apt-get install -y nginx
                    
                    # Start Nginx
                    sudo systemctl start nginx
                    
                    # Install prerequisites for Docker
                    sudo apt-get install -y ca-certificates curl
                    
                    # Add Docker's official GPG key
                    sudo install -m 0755 -d /etc/apt/keyrings
                    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
                    sudo chmod a+r /etc/apt/keyrings/docker.asc
                    
                    # Add Docker repository to Apt sources
                    echo \
                    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
                    $(. /etc/os-release && echo \"$VERSION_CODENAME\") stable" | \
                    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
                    
                    # Update package lists again to include Docker packages
                    sudo apt-get update
                    
                    # Install Docker packages
                    sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
                    
                    # Build Docker image
                    sudo docker build -t monyslim/pixer:latest .
                    
                    # Run Docker container
                    sudo docker run -d -p 801:80 monyslim/pixer:latest
                '''
            }
        }
    }
}
