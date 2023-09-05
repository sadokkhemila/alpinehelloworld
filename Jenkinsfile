pipeline{
    agent any
    environment {
        image_name = "alpineheloworld"
        image_tag = "latest"
    }

    stages {
        stage ('build image') {
           
            steps {
                script {
                    sh 'docker build -t test/$image_name:$image_tag .'
                }
            }
        }
        stage ('run container') {
            
            steps {
                script {
                    sh '''
                    docker run -d -p 80:5000 --name hello test/$image_name:$image_tag 
                    sleep 5 
                    '''
                }
            }
        }
        stage ('test container') {
            
            steps {
                script {
                    sh 'curl http://localhost | grep -q 'helloworld!' '
                }
            }
        }
    }
}
