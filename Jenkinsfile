node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                  // Don't Forget to give username and tokken to Jenkins
                  
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                      // give the configuration to git
                        sh "git config user.email ahmedatya1288@gmail.com"
                        sh "git config user.name AhmedAtiia11"
                      // Modify Deployment file with the new version "taken from the CI pipeline" 
                        sh "cat app/deployment.yaml"
                        sh "sh artifact_version_update app/deployment.yaml"
                        sh "echo $GIT_COMMIT_REV"
                        sh "cat app/deployment.yaml"
                      // MOdify the CD Repo with the new app  
                        sh "git add *"
                        sh "git commit -m 'Done by Jenkins Job changemanifest file: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Netfilx-Clone-CD/ HEAD:main"
                        // sh 'echo $GIT_USERNAME'
      }
    }
  }
}
}
