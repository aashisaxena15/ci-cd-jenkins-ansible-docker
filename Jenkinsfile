pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/aashisaxena15/ci-cd-jenkins-ansible-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('app') {
                    sh 'docker build -t my-flask-app:latest .'
                }
            }
        }

        stage('Save Image as Tar') {
            steps {
                sh 'docker save my-flask-app:latest > my-flask-app.tar'
            }
        }

        stage('Copy to Target Server') {
            steps {
                sh 'scp -i ~/.ssh/id_rsa my-flask-app.tar ubuntu@13.204.65.9:/tmp/'
            }
        }

        stage('Deploy via Ansible') {
            steps {
                sh 'ansible-playbook -i ansible/inventory.ini ansible/deploy.yml'
            }
        }
    }
}

