node {

    stage('Clean up') {
        bat """echo clean and delete file and directories"""
        cleanWs()
        // deleteDir()
    }

    stage('git clone') {
        // git branch: 'main', credentialsId: 'sct-git-credential', url: 'https://github.tools.sap/SCT/btp-data-model.git'
        // git branch: 'main', url: 'https://github.com/raibein/spring-test.git'
        git branch : 'main', credentialsId: 'sct-git-credential', url: 'https://github.tools.sap/SCT/btp-data-model.git'
        // bat """dir"""
    }

    stage('creating folder') {
        bat """mkdir data"""
    }

    // stage('creating txt file') {
    //     bat """echo 'Hello World!' >> readme.txt"""
    // }

    stage('copy to directory') {
        bat """xcopy sct-db\\data_test data /E"""
        // bat """cd data"""
        // bat """dir"""
    }

    stage('removed all except data') {
        // bat """del -R * -e data"""
        // bat """rmdir . /s /q"""
         
        bat """del -R ."""
        
        // bat """cd .."""
        // bat """dir"""
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
        bat """cd .."""
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