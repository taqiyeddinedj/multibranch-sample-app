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
                        -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion}\
                        versions:commit'
                    def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
                    def version = matcher[0][1] //index 0 will be the '<version>' itself and index 1 will be the version number
                    env.IMAGE_NAME = "$version-$BUILD_NUMBER"
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
                    echo "Building maven application."
                    sh 'mvn clean package'
                }
            }
        }

        stage('build Image') {
            steps {
                script {
                    echo "Building the app"
                    echo "Building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'dockr-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "docker build -t taqiyeddinedj/my-repo:${IMAGE_NAME} ."
                    sh " echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push taqiyeddinedj/my-repo:${IMAGE_NAME}"
                    }
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
