node {
    // Clean-up
    cleanWs()
    deleteDir()
    

    stage('git clone') {
        // git branch: 'main', credentialsId: 'git-token', url: 'https://github.tools.sap/SCT/btp-data-model.git'
        git branch: 'main', url: 'https://github.com/raibein/spring-test.git'
        git fetch : 'main', credentialsId: 'git-token', url: 'https://github.tools.sap/SCT/btp-data-model/sct-db'
        // bat """dir"""
    }

    // stage('creating folder') {
    //     bat """mkdir data"""
    // }

    // stage('creating txt file') {
    //     bat """echo 'Hello World!' >> readme.txt"""
    // }

    // stage('move file to folder') {
    //     bat """move readme.txt data"""
    //     bat """cd data"""
    //     bat """dir"""
    //     bat """dir data"""
    // }

    // stage('move folder to folder') {
    //     bat """move sct-db data"""
    //     bat """cd data"""
    //     bat """dir"""
    //     bat """dir data"""
    // }

    stage('mvn version') {
        bat """mvn -v"""
    }

    // stage('run mvn clean') {
    //     bat """mvn clean install"""
    // }

    stage('compile') {
        bat """mvn clean compile package"""
    }

    // stage('run mvn build spring boot') {
    //     bat """mvn spring-boot:run"""
    // }

    stage('list of files') {
        bat """dir"""
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