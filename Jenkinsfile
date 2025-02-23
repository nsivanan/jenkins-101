pipeline {
    agent cici-stratus-jenkins-slave

    environment {
        VENV_DIR = 'venv'  // Virtual Environment Directory
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
                sh 'source $VENV_DIR/bin/activate && python3 -m pip install --upgrade pip'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                source $VENV_DIR/bin/activate
                pip install -r requirements.txt
                '''
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
