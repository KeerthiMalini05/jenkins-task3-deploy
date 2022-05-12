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
                withDockerRegistry( [ credentialsId: "ecr:us-east-1:aws-credentials", url: "https://590852515231.dkr.ecr.us-east-1.amazonaws.com" ] ){
                sh 'docker run -d -p 8082:8080 590852515231.dkr.ecr.us-east-1.amazonaws.com/keerthi-jenkins-task3:$tagvalue'   
            }
        }
        }
      
        stage('QA_DEPLOY'){
            input{
                message "should approve ?"
                ok "Yes approve"
            }
            steps{
                echo 'deploy approved'
                withDockerRegistry( [ credentialsId: "ecr:us-east-1:aws-credentials", url: "https://590852515231.dkr.ecr.us-east-1.amazonaws.com" ] ){
                    sh 'docker run -d -p 8082:8080 590852515231.dkr.ecr.us-east-1.amazonaws.com/keerthi-jenkins-task3:$tagvalue'
                }
            } 
        }

        stage('CLEANUP'){
            steps{
                sh 'docker image prune -f --all'
            }
        }
    }
}
