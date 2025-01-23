pipeline {
    agent any
    stages {
        stage('Copy files to Docker server') {
            steps {
                script {
                    // Copy files to the remote Docker server
                    sh '''
                    # Using scp to copy files; ensure SSH key is accessible
                    scp -i ~/.ssh/id_rsa -r /var/lib/jenkins/workspace/neogym/* root@16.171.116.154:~/neogym
                    '''
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image on the remote server
                    sh '''
                    ssh -i ~/.ssh/id_rsa root@13.60.223.206 "cd ~/neogym && docker build -t neogym:latest ."
                    '''
                }
            }
        }
        stage('Create Docker Container') {
            steps {
                script {
                    // Check if the container exists, remove it if it does, then run a new container
                    sh '''
                    ssh -i ~/.ssh/id_rsa root@16.171.116.154 "
                    if docker ps -a --filter 'name=neogym_container' --format '{{.ID}}' | grep .; then
                        docker rm -f neogym_container
                    fi
                    docker run -d --name neogym_container -p 80:80 neogym:latest
                    "
                    '''
                }
            }
        }
    }
}
