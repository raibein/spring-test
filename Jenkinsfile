#!/usr/bin/env groovy

def checkingDIR() {

    File directory = new File('.\\db\\')

    directory.exists()

    return true
}


pipeline {

    agent any

    environment {
        SCT_GIT_CREDS = credentials('sct-git-credential')
        RABEN_GIT_CREDS = credentials('raben-git-creds')
    }
    
    stages {

        stage('Clean up') {
            steps {
                bat """echo clean and delete file and directories"""
                cleanWs()
                deleteDir()
            }
        }

        stage('Git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/raibein/spring-test.git'
                // git branch: 'main', credentialsId: 'sct-git-credential', url: 'https://github.tools.sap/SCT/btp-data-model.git'
            }
        }

        stage('Checking directory') {
            when {
                expression {
                    checkingDIR()
                }
            }
            steps {
                 bat """rmdir /s /q db"""
            }
        }

        stage('Creating Directories') {
            steps {
                bat """mkdir tmp"""
                bat """mkdir db\\src\\sct-provisioning-service\\sct_db\\"""
            }
        }

        stage('Download files from repo') {
            steps {
                withCredentials([string(credentialsId: 'sct-git-secret-text', variable: 'sct_secret')]) {
                    bat "cd tmp && git clone https://${SCT_GIT_CREDS_USR}:${sct_secret}@github.tools.sap/SCT/btp-data-model.git -b main"
                }
            }
        }

        stage('copy from tmp') {
            steps {
                bat """xcopy tmp\\btp-data-model\\sct-db\\data_test .\\db\\src\\sct-provisioning-service\\sct_db\\ /E"""
            }            
        }

        stage('Delete tmp') {
            steps {
                bat """rmdir /s /q tmp"""
            }
            // bat """del /s /q tmp"""
            // bat """rmdir . /s /q"""
        }

        // stage('mvn version') {
        //     bat """mvn -v"""
        // }

        // stage('run mvn clean') {
        //     bat """mvn clean install"""
        // }

        // stage('compile') {
        //     bat """mvn clean compile package"""
        // }

        // stage('run mvn build spring boot') {
        //     bat """mvn spring-boot:run"""
        // }

        stage('List of files') {
            steps {
                // bat """cd .."""
                bat """dir"""
            }
        }

        stage("Git config") {
            steps {
                bat"""
                    git config --global --add safe.directory ${env.WORKSPACE}
                    git config --global credential.helper wincred
                    git config --global user.name ${RABEN_GIT_CREDS_USR}
                    git config --global user.email "xraben5@gmail.com"
                    git config --global user.pass ${RABEN_GIT_CREDS_PSW}

                    git status
                    git checkout -b upload-data
                    git pull origin main
                """
            }
        }

        stage("Push to Git") {
            steps {
                bat """
                    echo ${RABEN_GIT_CREDS_USR}

                    git add .\\db\\src\\sct-provisioning-service\\sct_db\\
                    git commit -am "made changes"
                """

                // git tag ${currentBuild.startTimeInMillis}

                withCredentials([string(credentialsId: 'raben-git-secret-text', variable: 'raben_secret')]) {
                    bat "git push https://${RABEN_GIT_CREDS_USR}:${raben_secret}@github.com/raibein/spring-test.git -f"
                }

                // sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/my-org/my-repo.git')
                // git push origin main --repo https://${RABEN_GIT_CREDS_USR}:${RABEN_GIT_CREDS_PSW}@github.com/raibein/spring-test.git
            }
        }
    }
}