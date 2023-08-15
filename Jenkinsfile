pipeline {
    agent any
    tools {
        maven 'maven-3.9.4'
    }
    stages {

        stage('increment version'){
            steps {
                script {
                    echo "Incrementing app version"
                    sh 'mvn build-helper:parse-version versions:set \
                     -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${pasredVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion}\
                     versions:commit'
                }
            }
        }

        stage('test') {
            steps {
                script {
                    echo "Testing the application"
                    echo "Executing pipeline for branch $BRANCH_NAME"
                }
            }
        }

        stage('build Maven app') {
            steps {
                script {
                    echo "Building maven application"
                    sh 'mvn package'
                }
            }
        }
        
        stage('build Image') {
            steps {
                script {
                    echo "Building the app"
                    echo "Building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'dockr-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "docker build -t taqiyeddinedj/my-repo:jma-4.0 ."
                    sh " echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push taqiyeddinedj/my-repo:jma-4.0"
                }
            }
        }
        
        stage('deploy') {   
            steps {
                script {
                    echo "Deploying Docker image to EC2 instance"
                }
            }
        }
    }
}
}