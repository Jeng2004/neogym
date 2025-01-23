pipeline {
    agent any
    stages {
        stage("Checkout SCM") {
            steps {
                git url: 'https://github.com/Jeng2004/neogym.git', branch: 'main'
            }
        }

        stage("Prepare Workspace") {
            steps {
               // Create the admin directory on the Docker server
                sh "ssh root@13.60.67.78 'mkdir -p ~/admin'"
            }
        }

        stage("Copy files to Docker server") {
            steps {
                // Add debugging information
                sh "echo 'Listing files in the Jenkins workspace:'"
                sh "ls -la /var/lib/jenkins/workspace/neogym/"
                
                // Copy files using SCP
                sh "scp -o StrictHostKeyChecking=no -r /var/lib/jenkins/workspace/neogym/* root@13.60.67.78:~/admin"
            }
        }

        stage("Build Docker Image") {
            steps {
                // Invoke the Ansible playbook for building the Docker image
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/neogym/playbooks/build.yaml'
            }
        }

        stage("Create Docker Container") {
            steps {
                // Run the Ansible playbook for deploying the Docker container
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/neogym/playbooks/deploy.yaml'
            }
        }
    }
}
