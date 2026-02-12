pipeline {
    agent any

    environment {
        VENV = "venv"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Python') {
            steps {
                sh 'python3 -m venv $VENV'
                sh '. $VENV/bin/activate && pip install --upgrade pip'
                sh '. $VENV/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh '. $VENV/bin/activate && pytest --maxfail=1 --disable-warnings -q'
            }
        }
    }

    post {
        failure {
            echo "Build failed. Future: Send logs to self-healing system."
        }
        success {
            echo "Build succeeded."
        }
    }
}