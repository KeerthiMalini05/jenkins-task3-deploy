pipeline {
    agent any

    stages {
      
        stage('DEV_DEPLOY'){
            steps{
                sh 'mvn clean package'
                sh 'docker build -t keerthi-jenkins-task3:latest .'   
            }
        }
        stage('QA_DEPLOY'){
            input{
                message "should approve ?"
                ok "Yes approve"
            }
            steps{
                echo 'deploy approved'
            } 
        }

        stage('CLEANUP'){
            steps{
                docker image prune --all
            }
        }
    }
}
