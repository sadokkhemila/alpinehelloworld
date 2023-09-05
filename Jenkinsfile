pipeline{
    agent any
    environment {
        image-name = "alpineheloworld"
        image-tag = "latest"
    }

    stages {
        stage ('build image') {
           
            steps {
                script {
                    sh 'docker build -t test/$image-name:$image-tag .'
                }
            }
        }
        stage ('run container') {
            
            steps {
                script {
                    sh '''
                    docker run -d -p 80:5000 -- name hello test/$image-name:$image-tag 
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
