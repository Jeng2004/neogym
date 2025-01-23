pipeline {
    agent any
    stages {      
        stage("Copy file to Docker server") {
            steps {
                                // Debugging step to list files before the copy
                sh "echo 'Listing files in the admin directory:'"
                sh "ls -la /var/lib/jenkins/workspace/admin/"
                
                // Proceed with scp command
                sh "scp -r /var/lib/jenkins/workspace/admin/* root@16.171.116.154:~/admin"
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
