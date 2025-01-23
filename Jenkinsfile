pipeline {
    agent any
    stages {      
        stage("Copy file to Docker server") {
            steps {
                // Ensure the source directory is correct
                sh "scp -r /var/lib/jenkins/workspace/admin/* root@13.60.67.78:~/admin"
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
