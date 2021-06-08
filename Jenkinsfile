node{
    stage('git checkout'){
        git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/swapanGit/nodejsDemo.git'
    }
    stage('install npm'){
        nodejs('nodeJs') {
            sh'npm install'
        }
    }
    stage('install npm'){
        nodejs('nodeJs') {
            sh'npm test'
        }
    }
}
