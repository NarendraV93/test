pipeline {
    agent any

    environment {
        JOB_NAME = 'Demo_Job'
        IMAGE_NAME = 'python'
        USER = 'narendrav1893'
        TAG = 'v1893'
        
    }
    
    stages {

        stage('Build a docker image, push it to Registry & Run the container') {
            steps {
                script {
			   
                   if (env.BRANCH_NAME.startsWith("main")) {
                       withCredentials([string(credentialsId: 'docker_login_passwd', variable: 'var1')]) {
                       sh "cd /var/lib/jenkins/workspace/${JOB_NAME}_${env.BRANCH_NAME}"
                       sh 'docker login -u=${USER} -p="${var1}"'                  
                       sh 'docker build -t ${USER}/${IMAGE_NAME}:${TAG} .'
                       sh "docker push ${USER}/${IMAGE_NAME}:${TAG}"
		       sh "docker run -d -p 5000:5000 ${USER}/${IMAGE_NAME}:${TAG}"
                      } 

                  } 
                }

            }
        
        }
     }

}
