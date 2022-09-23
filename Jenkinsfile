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
                // deleteDir()
            }
        }

        stage('git clone') {
            steps {
                git branch: 'main', url: 'https://github.com/raibein/spring-test.git'
                // git branch: 'main', credentialsId: 'sct-git-credential', url: 'https://github.tools.sap/SCT/btp-data-model.git'
            }
        }

        stage('creating tmp folders') {
            steps {
                bat """mkdir tmp"""
                bat """mkdir db\\src\\sct-provisioning-service\\sct_db\\"""
            }
        }

        stage('download files from repo') {
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

        stage('del tmp') {
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

        stage('list of files') {
            steps {
                // bat """cd .."""
                bat """dir"""
            }
        }

        // stage("Commit") {
        //     bat('''
        //         git checkout -B $TARGET_BRANCH
        //         // git config user.name 'my-ci-user'
        //         // git config user.email 'my-ci-user@users.noreply.github.example.com'
        //         git add . && git commit -am "[Jenkins CI] Add build file"
        //     ''')
        // }

        stage("Push") {
            steps {
                bat """
                    echo ${RABEN_GIT_CREDS_USR}
                    git config --global --add safe.directory \\.
                    git config --global user.name ${RABEN_GIT_CREDS_USR}
                    git config --global user.pass ${RABEN_GIT_CREDS_PSW}

                    git pull origin main
                    git checkout main
                    git add .
                    git commit -m 'made changes'
                    git push origin main
                """

                // git push origin main --repo https://${RABEN_GIT_CREDS_USR}:${RABEN_GIT_CREDS_PSW}@github.com/raibein/spring-test.git
            }
        }
    }
}