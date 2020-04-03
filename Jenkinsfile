pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './mvnw compile'
      }
    }

    stage('Test') {
      steps {
        sh './mvnw test'
      }
    }
    
    stage('Package') {
      steps {
        sh './mvnw package'
      }
    }
    stage('Deploy') {
      git_branch_local=$(echo $GIT_BRANCH   | sed -e "s|origin/||g")
      echo GIT_BRANCH_LOCAL=$git_branch_local > build.properties
      when {
        expression {${git_branch_local} == 'master'}
      }
                    steps {
                      sh './mvnw deploy'
                    }
    }

  }
   post {
    	failure {
emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n Has failed. recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build failed"
     	}
     success {
     emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n has succeeded. recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build succeeded"

     }
   }

}
