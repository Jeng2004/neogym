pipeline {
    agent any
    stages {
        stage("Checkout SCM") {
            steps {
                git url: 'https://github.com/Jeng2004/neogym.git'
            }
        }

        stage("Prepare Workspace") {
            steps {
                // Ensure the admin directory exists on the remote Docker server
                sh "mkdir -p /var/lib/jenkins/workspace/admin"
            }
        }

        stage("Copy files to Docker server") {
            steps {
                // Add debugging information
                sh "echo 'Listing files in the Jenkins workspace:'"
                sh "ls -la /var/lib/jenkins/workspace/neogym/"
                
                // Use SCP command, making sure to disable strict host key checking for testing purposes
                sh "scp -o StrictHostKeyChecking=no -r /var/lib/jenkins/workspace/neogym/* root@13.60.67.78:~/admin"
            }
        }

        stage("Build Docker Image") {
            steps {
                // Example of invoking Ansible playbook
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/neogym/playbooks/build.yaml'
            }
        }

        stage("Create Docker Container") {
            steps {
                // Ensure the correct path to the Ansible playbook
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/neogym/playbooks/deploy.yaml'
            }
        }
    }
}
