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
                    // Build the Docker image from the Dockerfile in the repository
                    ansiblePlaybook playbook: '/var/lib/jenkins/workspace/neogym/playbooks/build.yaml'
                }
            }
        }

        stage("Deploy Docker Container") {
            steps {
                ansiblePlaybook playbook: '/var/lib/jenkins/workspace/neogym/playbooks/deploy.yaml'
            }
        }
    }
}
