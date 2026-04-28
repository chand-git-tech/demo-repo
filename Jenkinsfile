pipeline {
    agent any

    stages {

        stage('Build Image') {
            steps {
                sh 'podman build -t myapp:${BUILD_NUMBER} .'
                sh 'podman tag myapp:${BUILD_NUMBER} myapp:latest'
            }
        }

        stage('Save Image') {
            steps {
                sh 'rm -f myapp.tar'
                sh 'podman save -o myapp.tar myapp:latest'
            }
        }

        stage('Copy to Remote') {
            steps {
                sh 'scp myapp.tar john@10.89.27.71:/tmp/'
            }
        }

        stage('Deploy via Ansible') {
            steps {
                sh 'ansible-playbook -i inventory deploy.yml'
            }
        }

        stage('Test') {
            steps {
                sh 'curl http://<10.89.27.71>:8081'
            }
        }
    }
}
