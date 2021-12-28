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

    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }

    stage('Security Scan') {
      steps {
        {          aqua locationType: 'local', localImage: 'alpine', hideBase: false, notCompliesCmd: '', onDisallowed: 'ignore', showNegligible: false          }
      }
    }

    stage('Upload to AWS') {
      steps {
        withAWS(region: 'us-west-2', credentials: '990fd3fa-8e8f-47d9-973f-12f3fd7a0b47') {
          sh 'echo "Uploading content with AWS creds"'
          s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', bucket: 'accessiblehighlywebsite')
        }

      }
    }

  }
}
