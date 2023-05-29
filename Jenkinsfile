pipeline {
  agent any
  tools {
    go '1.19.9'
  }
  stages {

    stage('Checkout SCM') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [
            [name: 'master']
          ],
          userRemoteConfigs: [
            [
              url: 'https://github.com/jayvardhan2111/web_app.git',
              credentialsId: '',
            ]
          ]
        ])
      }
    }

    stage('Build') {
      steps {
        echo 'Building application...'
        sh 'go build ./web_app.go'
      }
    }
    // Add more stages as needed

    stage('Test') {
steps {

echo 'Testing application...'
sh './web_app &'
sh '''response=$(curl -s -o /dev/null -w "%{http_code}" http://localhost:80) &&
echo Resoince is: $response &&
[ "$response" = "200" ] && exit 0 || exit 1'''
}
}
}
}
