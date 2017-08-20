
pipeline {
    
    agent { node { label 'agent1' } }
    stages {
        stage('Build') {
            
            steps {
                git "https://github.com/vforv/hapi-seneca-ts"
                sh '''
                  ./system/fuge/ci/docker-up.sh
                  ./system/fuge/ci/docker-down.sh
                '''
            }
        }
        
        stage('Test') {
            steps {
                sh '''
                 rm -rf system/fuge/test
                 ./system/fuge/ci/docker-up-test.sh
                 chown -R master:master system/fuge/test
               '''
            }
        }
    }
    
        post {
          always {
            junit 'system/fuge/test/*.xml'
          }
        }
    
}