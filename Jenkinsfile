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
                    // Build the Docker image
                    sh "docker build -t neogym:latest /var/lib/jenkins/workspace/neogym"
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
