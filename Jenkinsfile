pipeline {

    agent any

    environment {
        SCT_GIT_CREDS = credentials('sct-git-credential')
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
                bat """xcopy tmp\\btp-data-model\\sct-db\\data_test .\\data-test /E"""
            }            
        }

        // stage('removed all except data') {
        //     // bat """del -R * -e data"""
        //     // bat """rmdir . /s /q"""
            
        //     bat """rmdir /s /q tmp"""
            
        //     // bat """cd .."""
        //     // bat """dir"""
        // }

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

        // stage("Push") {
        //     environment { 
        //         GIT_AUTH = credentials('support-team-up') 
        //     }
        //     bat('''
        //             git config --local credential.helper "!f() { echo username=\\$GIT_AUTH_USR; echo password=\\$GIT_AUTH_PSW; }; f"
        //             git push origin HEAD:$TARGET_BRANCH
        //     ''')
        // }
    }
}