pipeline {
    agent any
    stages {
        stage("Checkout SCM") {
            steps {
                git url: 'https://github.com/Jeng2004/neogym.git', branch: 'main'
            }
        }

        stage("Build Docker Image") {
            steps {
                script {
                    // Use Ansible to build the Docker image
                    ansiblePlaybook playbook: '/var/lib/jenkins/workspace/neogym/playbooks/build.yaml'
                }
            }
        }

        stage("Deploy Docker Container") {
            steps {
                // Use Ansible to deploy the Docker container
                ansible-playbook /var/lib/jenkins/workspace/neogym/playbooks/deploy.yaml
            }
        }
    }
}
