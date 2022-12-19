pipeline{
    agent any
    tools{
        maven 'maventest'
    }
    stages{
        stage('git checkout'){
            steps{
                git credentialsId: 'github-id',url:'https://github.com/dayana-18/tp7-pipeline.git'
            }
        }
        
        stage('build the application'){
            steps{
                sh 'mvn clean install'
            }
        }
        
        stage('Unit Test Execution') {
            steps{
                sh 'mvn test'
            }
        }
        
        stage('Build the docker image') {
            steps{
                withCredentials([usernamePassword(credentialsId:'dockerhub-id', usernameVariable:'dockerHubId', passwordVariable:'dockerHubPass')]) {
                    sh "docker login -u $dockerHubId -p $dockerHubPass"
                }
                sh 'docker build --tag dada/triangle .'
            }
        }
    }
}