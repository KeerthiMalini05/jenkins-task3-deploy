pipeline {
    agent any

    stages {
        
        stage('DEV_DEPLOY') {


            steps {

                script {
                        CHOICES = ["tag1", "tag2", "tag3"];    
                        env.YourTag = input  message: 'What are we deploying today?',ok : 'Deploy',id :'tag_id',
                                        parameters:[choice(choices: CHOICES, description: 'Select a tag for this build', name: 'TAG')]
                        }           
                sh 'mvn clean package'
                sh 'docker build -t keerthi-jenkins-task3:${env.YourTag} .'
                echo "Deploying ${env.YourTag}. Have a nice day."
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
                sh 'docker image prune --all'
            }
        }
    }
}
