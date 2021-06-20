node{
    stage('git checkout'){
        git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/swapanGit/nodejsDemo.git'
    }
   stage('Review node and npm installations') {
	steps {
		nodejs(nodeJSInstallationName: 'node13') {
		sh 'npm -v'  
		sh 'node -v'
			}
		}
	}
	stage('Downloading dependencies') {
        sh 'npm install'
    }
	stage('Testing') {
        sh 'npm test'
    }
   stage('Build Docker Image'){
     sh 'docker build -t <docker-user-name>/my-app:2.0.0 .'
   }
   stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u <docker-user-name> -p ${dockerHubPwd}"
     }
     sh 'docker push <docker-user-name>/my-app:2.0.0'
   }
    stage('Run Container on Dev Server'){
     sh 'docker run -p 8080:8080 -d --name my-app <docker-user-name>/my-app:2.0.0'
   }
    stage ('Kubernetes Deployment') {
        kubernetesDeploy(
            configs: 'MyApp/springBootDeploy.yml',
            kubeconfigId: 'K8S',
            enableConfigSubstitution: true
            )
    }
}
