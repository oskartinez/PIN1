pipeline {
  agent 'maven'

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
    NEXUS_URL = "192.168.0.21:8083"
  }
   stages {
   stage('Building image') {
      steps{
          sh '''
             docker build -t testapp .
             '''  
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }
   stage('Deploy Image') {
      steps{
        sh '''
        docker login ${NEXUS_URL} -u dockeruser -p holamundo123
        docker image tag testapp ${NEXUS_URL}/dockeruser/testapp:1.0
        docker image push ${NEXUS_URL}/dockeruser/testapp:1.0
        '''
        }
      }
    }
}


    
  

