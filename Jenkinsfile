pipeline {
    agent {label 'cici-stratus-jenkins-slave'}

    environment {
        VENV_DIR = 'venv_python'  // Virtual Environment Directory
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/nsivanan/jenkins-101.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh 'python3 -m venv $VENV_DIR'
                sh 'bash -c "source venv_python/bin/activate && python --version"'
                sh 'sudo apt install python3-pip'
                sh 'pip list'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'bash -c "source venv_python/bin/activate"'
                sh 'python3 -m pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'source $VENV_DIR/bin/activate && pytest tests/'
            }
        }

        stage('Deploy') {
            steps {
                sh 'source $VENV_DIR/bin/activate && python3 helloworld.py'
            }
        }
    }

    post {
        success {
            echo '✅ Build and deployment completed successfully!'
        }
        failure {
            echo '❌ Build failed. Check logs for errors.'
        }
    }
}
