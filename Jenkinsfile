pipeline {

   agent any



   stages {
    
    stage('build docker image'){
        steps {
            script {
                sh 'docker build -t "ahlawsahla" . '
            }
        }

    }

    stage ('run nginxcontainer'){
        steps {
            script{
                sh 'docker run -d -p 8089:80 ahlawsahla'
            }
        }
    }


   }



}
