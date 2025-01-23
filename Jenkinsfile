pipeline {
    agent any
    stages {
        stage('Copy file to Docker server') {
            steps {
                sh '''
                scp -i ~/.ssh/id_rsa -r /var/lib/jenkins/workspace/neogym/* root@16.171.116.154:~/neogym
                '''
            }
        }
        stage('Build Docker Image') {
            steps {
                sh '''
                ssh -i ~/.ssh/id_rsa root@13.60.223.206 "cd ~/neogym && docker build -t neogym ."
                '''
            }
        }
        stage('Create Docker Container') {
            steps {
                sh '''
                ssh -i ~/.ssh/id_rsa root@16.171.116.154 "
                if docker ps -a --filter 'name=neogym_container' --format '{{.ID}}' | grep .; then
                    docker rm -f neogym_container
                fi
                docker run -d --name neogym_container -p 80:80 neogym_image
                "
                '''
            }
        }
    }
}
