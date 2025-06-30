pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
                sh 'ls -la'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest --verbose test_app.py'
            }
        }

        stage('Notify Success') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo('SUCCESS') }
            }
            steps {
                echo 'Tests passed!'
            }
        }

        stage('Notify Failure') {
            when {
                expression { currentBuild.resultIsWorseThan('SUCCESS') } 
            }
            steps {
                echo 'Pipeline failed! Check test results.'
            }
        }
    }

    post {
        always {
            echo "Pipeline completed with status: ${currentBuild.result}"
        }
    }
}