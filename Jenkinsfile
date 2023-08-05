pipeline {
    agent any
    tools {
        maven 'maven-3.9.4'
    }
    stages {
        stage('build JAR') {
            steps {
                script {
                    echo "Building the application..."
                    sh 'mvn package'

                }
            }
        }

        stage('build Docker image') {
            steps {
                script {
                    echo "Building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'dockr-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t taqiyeddinedj/my-repo:jma-2.0 .'
                        sh " echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push taqiyeddinedj/my-repo:jma-2.0'
                    }

                }
            }
        }

        stage('deploy') {         
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }
    }
}
