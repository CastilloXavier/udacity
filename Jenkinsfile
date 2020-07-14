pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
         stage('Security Scan') {
              steps {
                aquaMicroscanner imageName: 'alpine: latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail'
              }
         } 
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-east-2', credentials:'e7e7a7be-ac27-41f1-a724-33663eecae7f') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'static-jenkins-pipelinee')
                  }
              }
         } 
     }
}
