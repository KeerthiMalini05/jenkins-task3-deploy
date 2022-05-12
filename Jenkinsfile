pipeline {
    agent any

    stages {
        
        stage('PROMPT INPUT') {
            steps {
                script {
                         env.tagvalue = input message: 'Please enter the build tag value',
                             parameters: [string(defaultValue: '',
                                          description: '',
                                          name: 'tagvalue')]
                        }           
              
            }
        }
        
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
                sh 'docker image prune -f --all'
            }
        }
    }
}
