#!/usr/bin/env groovy 

@Library('jenkins-shared-library') //in case we dont have any vriable declaration after this line we would have to add _ 'underscore' after the library name
def gv                             //@Library('jenkins-shared-library')_

pipeline {
    agent any
    tools {
        maven "maven-3.9.4"
    }
    stages {
        stage('init') {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }

        stage('build jar') {
            steps {
                script {
                    buildJar()
                }
            }
        }

        stage('build image') {
            steps {
                script {
                    buildImage()
                }
            }
        }

        stage('deploy') {
            steps {
                script {
                    gv.deployApp()
                   
                }
            }
        }
    }
}