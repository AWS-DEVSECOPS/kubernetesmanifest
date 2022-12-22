pipeline{
agent any

options{
timestamps()
buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '3', daysToKeepStr: '', numToKeepStr: '3'))
}
stages{
stage('Clone repository') {
 checkout scm
    }
    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'githubtoken', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                       // def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email arjunprodev@gmail.com"
                        sh "git config user.name arjundevsecops"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+arjundevsecops/mavenrepo.*+arjundevsecops/mavenrepo:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/AWS-DEVSECOPS/kubernetesmanifest.git HEAD:master"
      }
    }
  }
}
}


