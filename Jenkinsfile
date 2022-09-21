node {
    // Clean-up
    cleanWs()
    deleteDir()
    

    // stage('get git repo') {
    //     git branch: 'main', credentialsId: 'git-token', url: 'https://github.tools.sap/SCT/btp-data-model.git'
    //     bat """dir"""
    // }

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

    stage('test mvn version') {
        bat """mvn -v"""
    }

    // stage('run mvn clean') {
    //     bat """mvn clean install"""
    // }

    stage('run mvn clean') {
        bat """mvn clean compile package"""
    }

    // stage('run mvn build spring boot') {
    //     bat """mvn spring-boot:run"""
    // }
}