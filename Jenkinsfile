pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'podman build -t myapp:v1 .'
            }
        }

        stage('Deploy') {
            steps {
                sh 'podman stop myapp || true'
                sh 'podman rm myapp || true'
                sh 'podman run -d -p 8081:80 --name myapp myapp:v1'
            }
        }

        stage('Test') {
            steps {
                sh 'curl -f http://localhost:8081'
            }
        }
    }
}
