pipeline {
    agent any
    stages {      
        stage("Copy file to Docker server") {
            steps {                // Create admin directory if it doesn't exist
                sh "mkdir -p /var/lib/jenkins/workspace/admin"
                
                // List and copy from the appropriate path
                sh "echo 'Listing files in the Jenkins workspace:'"
                sh "ls -la /var/lib/jenkins/workspace/neogym/"
                
                // Use the correct path based on your repo structure
                sh "scp -r /var/lib/jenkins/workspace/neogym/* root@16.171.116.154:~/admin"
            }
        }
        
        stage("Build Docker Image") {
            steps {
                // Path to your Ansible playbook for building the Docker image
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/admin/playbooks/build.yaml'
            }    
        } 
        
        stage("Create Docker Container") {
            steps {
                // Path to your Ansible playbook for deploying the Docker container
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/admin/playbooks/deploy.yaml'
            }    
        }
    }
}
