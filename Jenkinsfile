def remote = [:]
remote.name = 'test'
remote.host = '43.204.38.247'
remote.port = 22
remote.allowAnyHosts = true

pipeline {
    agent any
     stages {
        stage('Git Clone') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', credentialsId: 'GitHubCred', url: 'https://github.com/Khanshoyeb7/demojen.git'
            }
        }
     stage('Deployment'){
        steps {
            script {
             // move the new changed
             withCredentials([usernamePassword(credentialsId: 'LinuxCred', passwordVariable: 'pass', usernameVariable: 'user')]) {
             remote.user = user
             remote.password = pass
             sshPut remote: remote, from: "index.html", into: "/var/www/html"
             sshCommand remote: remote, command: "ls /var/www/html
             }
           }
          }
        }
      }
    }
