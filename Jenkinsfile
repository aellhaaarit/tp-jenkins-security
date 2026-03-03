pipeline {
    agent any

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'python3 -m pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('SCA Scan') {
            steps {
                sh '''
                dependency-check.sh \
                --project "TP-Jenkins" \
                --scan . \
                --format HTML \
                --failOnCVSS 7
                '''
            }
        }
    }

    post {
        failure {
            echo 'Build failed due to vulnerabilities or errors'
        }
    }
}