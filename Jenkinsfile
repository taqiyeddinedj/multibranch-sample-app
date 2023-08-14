pipeline {
    agent any

    stages {
        stage('test') {
            steps {
                script {
                    echo "Testing the aplication"
                    echo "Executing pipeline for branch $BRANCH_NAME"
                }
            }
        
        stage('build') {
            when {
                expression {
                    BRANCH_NAME == 'master'
                }
            }
            steps {
                script {
                    echo "Building the app"
                }
            }
        }
        stage('dploy') {
            when {
                expression {
                    BRANCH_NAME == 'master'
                }
            }
            steps {
                script {
                    echo "Deploying the app"
                }
            }
        }

        }

    }
}
